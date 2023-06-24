---
title: "C Encrypt Decrypt"
description: "OpenSSL usage in C with ChatGPT help."
lead: "OpenSSL usage in C with ChatGPT help."
date: 2023-01-28T14:33:37+01:00
lastmod: 2023-01-28T14:33:37+01:00
draft: false
images: []
menu:
  docs:
    parent: "tools"
    identifier: "c-encrypt-decrypt-df40ff70025e2e862073d7fceda23776"
weight: 999
toc: true
---

-fu with C language

I never really liked C or C++, but we'll focus on C. This article is about how big trouble is to get things done when you have limited resources available on the web, and only one friend - `ChatGPT`.

## Idea

I want to easily encrypt and decrypt a message. May it be a file, may it be a string. I wan't to hide it from general public. I wan't to seamlessly get the meaning from cipher text, when I have the proper credentials.

Something like this:

```shell
nutek-ccrypt -e "I love you 👩‍❤️‍👨"
Password:
cipher-text
```

Then my love will use our secret password to decrypt this cryptic slogan:

```shell
nutek-ccrypt -d cipher-text
Password:
I love you 👩‍❤️‍👨
```

## Problem

Unfortunately, `Rust` can't be installed on my developer machine, so I have to use something different. I never used `C`... Let's go with that! This is only starting Linux environment with "Development Tools" or build-essentials installed.

### Knock... knock...

This is **OpenAI**, we have a _friend_ for you, so you might ask him what's your trouble and he will give you answers to all your questions (as long as they are in the non rush hours). He is not very precise, but he is very well thaught in the english language and is a fair companion for semi-creative (aka lazy) ppl who like to bites own tail in a whirlwind of chat sequences. That's it - it's **free** - no hug ;)

## Ask first, punch later

Long story short, after few days of fighting for bandwidth with US citizens, many iterations, and questions to ChatGPT, it kindly provided me with somehow good answer to my question - how to encrypt and properly decrypt a text message?

### Encrypt text message

We will use password, salt, deriving key from password and a salt, then using this key to encrypt message. Everything in buffers of data, no high level approach, just strict calls to OpenSSL library. After few days of tackling this problem, I know that there are many ways to write the same functionality, and some are better to maintain and understand. So here it goes. My full encrypt function:

### Include

include openssl libraries
include basic c libraries

```c
#include <openssl/evp.h>
#include <openssl/rand.h>
#include <openssl/kdf.h>
#include <stdio.h>
#include <string.h>
```

### OpenSSL fields for key and block size

define some fields that will be used in deriving key and in
buffer manipulation

```c
#define AES_KEY_SIZE 256
#define AES_BLOCK_SIZE 16
#define SALT_SIZE 8
#define ITERATIONS 10000
#define HASH_SIZE 32
```

### Encrypt function signature

I take input file, output file and a password as arguments to
encrypt function.

```c
int encrypt_it(const char *input_file, const char *output_file, const char *password) {
```

### Open files for input and output

Open input and output files

```c
// rb stands for read binary mode
FILE *f = fopen(input_file, "rb");
if (!f) {
    printf("error opening input file\n");
    return -1;
}

// wb stands for write binary mode
FILE *of = fopen(output_file, "wb");
if (!of) {
    printf("error opening output file\n");
    return -1;
}
```

### Initialization Vector:

is a random number that is used along with a secret key for data encryption.

```c
// Generate a random IV with specified size
unsigned char iv[AES_BLOCK_SIZE];
RAND_bytes(iv, AES_BLOCK_SIZE);

// Write the IV to the output file
fwrite(iv, 1, AES_BLOCK_SIZE, of);
```

```c
    // Generate a salt
    unsigned char salt[SALT_SIZE] = "stranger";
    // if you uncomment next two lines, you have to provide
    // salt to decrypt function, or simply to derive a key
    // you could attach it to password or something like that
    // RAND_bytes(salt, SALT_SIZE);
    // strcpy(salt, (unsigned char)"stranger");

    // Derive the key from the password
    unsigned char key[HASH_SIZE];
    PKCS5_PBKDF2_HMAC(password, strlen(password), salt, SALT_SIZE, ITERATIONS, EVP_sha256(), HASH_SIZE, key);

    // Create a new cipher context
    EVP_CIPHER_CTX *ctx = EVP_CIPHER_CTX_new();
    if (!ctx) {
        printf("error creating cipher context\n");
        return -1;
    }

    // Set the encryption algorithm and key
    if (EVP_EncryptInit_ex(ctx, EVP_aes_256_cbc(), NULL, key, iv) != 1) {
        printf("error initializing encryption\n");
        return -1;
    }

    // Set the padding method to PKCS7
    EVP_CIPHER_CTX_set_padding(ctx, EVP_PADDING_PKCS7);

    // Read data from the input file in blocks of AES_BLOCK_SIZE
    unsigned char buffer[AES_BLOCK_SIZE];
    int out_len;
    while (fread(buffer, 1, AES_BLOCK_SIZE, f) > 0) {
        // Encrypt the data
        if (EVP_EncryptUpdate(ctx, buffer, &out_len, buffer, AES_BLOCK_SIZE) != 1) {
            printf("error encrypting data\n");
            return -1;
        }

        // Write the encrypted data to the output file
        fwrite(buffer, 1, out_len, of);
    }

    // Pad any remaining data
    int padded_len;
    if (EVP_EncryptFinal_ex(ctx, buffer, &padded_len) != 1) {
        printf("error finalizing encryption\n");
        return -1;
    }

    // Write the padded data to the output file
    fwrite(buffer, 1, padded_len, of);

    // Clean up
    EVP_CIPHER_CTX_free(ctx);
    fclose(f);
    fclose(of);

    return 0;
}%
```

And encryption works like a charm (_maybe not?_). It's even padding the rest of the last buffer and ends with a number of padded bytes, but hold your horses. You have to decrypt this message. And here comes the devil inside those tiny details. Those padded bytes aren't actually easily removed from deciphered message. But first how?

### Decryption algorithm that does not cut on padded bytes

```c
#include <stdio.h>
#include <openssl/aes.h>
#include <openssl/kdf.h>
#include <string.h>

int decrypt_it(const char *input_file, const char *output_file, const char *password) {
    // Open input and output files
    FILE *f = fopen(input_file, "rb");
    if (!f) {
        printf("error opening input file\n");
        return -1;
    }

    FILE *of = fopen(output_file, "wb");
    if (!of) {
        printf("error opening output file\n");
        return -1;
    }

    // Read the IV from the input file
    unsigned char iv[AES_BLOCK_SIZE];
    if (fread(iv, 1, AES_BLOCK_SIZE, f) != AES_BLOCK_SIZE) {
        printf("error reading IV\n");
        return -1;
    }

    // Generate a salt
    unsigned char salt[SALT_SIZE] = "stranger";
    // RAND_bytes(salt, SALT_SIZE);
    // strcpy(salt, "stranger");

    // Derive the key from the password
    unsigned char key[HASH_SIZE];
    PKCS5_PBKDF2_HMAC(password, strlen(password), salt, SALT_SIZE, ITERATIONS, EVP_sha256(), HASH_SIZE, key);

    // Create a new cipher context
    EVP_CIPHER_CTX *ctx = EVP_CIPHER_CTX_new();
    if (!ctx) {
        printf("error creating cipher context\n");
        return -1;
    }

    // Set the decryption algorithm and key
    if (EVP_DecryptInit_ex(ctx, EVP_aes_256_cbc(), NULL, key, iv) != 1) {
        printf("error initializing decryption\n");
        return -1;
    }

    // Set the padding mode to PKCS7
    EVP_CIPHER_CTX_set_padding(ctx, EVP_PADDING_PKCS7);

    // Read the input file and decrypt it
    unsigned char buffer[BUFSIZ];
    int len;
    while ((len = fread(buffer, 1, sizeof buffer, f)) > 0) {
        int out_len;
        if (EVP_DecryptUpdate(ctx, buffer, &out_len, buffer, len) != 1) {
            printf("error during decryption\n");
            return -1;
        }
        fwrite(buffer, 1, out_len, of);
    }

  // take buffer length
    int buffer_length = strlen((char *)buffer);

    // Create a command to run the Perl script and pass the buffer as input
    char command[100];
    snprintf(command, sizeof(command), "perl truncate_buffer.pl < %s", buffer);

    // Execute the command and redirect the output to a variable
    char truncated_buffer[buffer_length];
    FILE* fp = popen(command, "r");
    fgets(truncated_buffer, buffer_length, fp);
    pclose(fp);

    // printf("Original buffer: %s\n", buffer);
    // printf("Truncated buffer: %s\n", truncated_buffer);

  // event this does not help
    fwrite("\n\0", sizeof(char), 2, of);

    // Finalize the decryption
    // moved from before perl script invocation,
    // because maybe that was the problem?
    int out_len;
    if (EVP_DecryptFinal_ex(ctx, buffer, &out_len) != 1) {
        printf("error during finalization\n");
        return -1;
    }
    fwrite(buffer, 1, out_len, of);

    // Clean up
    EVP_CIPHER_CTX_free(ctx);
    fclose(f);
    fclose(of);

    return 0;
}%
```

## Cheat with Perl

So I thought that it would be smart, if nothing else works... To use _Perl_. But still. DRE.

```perl
#!/usr/bin/env perl

 the buffer from standard input
$buffer = <STDIN>;

 the last byte of the buffer
$last_byte = substr($buffer, -1, 1);

 the last byte to an integer
$truncate_length = ord($last_byte);

 the buffer
$truncated_buffer = substr($buffer, 0, length($buffer) - $truncate_length);

 the truncated buffer to standard output
print $truncated_buffer;
```

## Even weirder main() function

```c
#include <stdio.h>
#include <stdlib.h>
#include <stddef.h>
#include <string.h>
// get command line arguments and create simple
// parser
#include <getopt.h>
#include <openssl/evp.h>
#include <openssl/rand.h>
#include <unistd.h>
#include <termios.h>

// I tried to get this done for couple of days
// this is the evidence
// #include "encrypt.c"
// #include "decrypt.c"

// this is the righ files
#include "en.c"
#include "de.c"

#define BUFSIZE 4096

// some function signatures
void print_help(char *argv);
void get_password(char *s);

// null termination charater at the end of string
// some said it helps
unsigned char *null_term(unsigned char *text) {
    size_t len = strlen((char *)text);
    unsigned char *new_bigger = (unsigned char *)malloc(len + 1);
    memcpy(new_bigger, text, len);
    new_bigger[len] = '\0';
    return new_bigger;
}

// here it starts
int main(int argc, char *argv[])
{
    int opt;
    // check for -h -e and -d command line arguments
    while ((opt = getopt(argc, argv, "hed")) != -1) {
        // size of password
        char s[32];
        int bytes_written;
        switch (opt) {
        case 'h':
            print_help(argv[0]);
            return 0;
            break;
        case 'e':
            if (argc == 4) {
                get_password(s);
                bytes_written = encrypt_it(argv[2], argv[3], s);
            // this is garbage in this else...
            // I try to make inline encryption...
            // ChatGPT is not a good teacher for my kind of personality
            // Lots of trial and error. It worked before. But then,
            // I wanted it to work with files good,
            // and then I broke this and the decrypt it counterpart too.
            // works for files, not inline
            // TODO
            } else if (argc == 3) {
                get_password(s);
                char *cli = argv[2];
                FILE *f;
                f = fopen("clear_encrypt", "w");
                fwrite(cli, sizeof(char), strlen(cli), f);
                fclose(f);
                unsigned char buffer[BUFSIZ];
                bytes_written = encrypt_it("clear_encrypt", "cipher_encrypt", s);
                f = fopen("cipher_encrypt", "rb");
                size_t bytes_read;
                while ((bytes_read = fread(buffer, 1, sizeof buffer, f)) > 0) {
                    // char hex_iv[bytes_read*2+1];
                    // OPENSSL_buf2hexstr_ex(hex_iv, bytes_read * 2, NULL, buffer, bytes_read, '\0');
                    // for (int i = 0; i < sizeof(hex_iv); i++) {
                    //     printf("%s", hex_iv[i]);
                    // }
                    char binary_data[] = "my share has been to good learn";
                    char command[100];
                    sprintf(command, "perl -e 'print unpack(\"H*\", \"%s\")'", binary_data);
                    FILE *fp = popen(command, "r");
                    if (fp == NULL) {
                        printf("Failed to execute command\n");
                        exit(1);
                    }
                    char output[bytes_read*2+1];
                    fgets(output, sizeof(output), fp);
                    printf("%s", output);
                    pclose(fp);
                    // printf("%s", hex_iv);
                    // for (int i = 0; i < bytes_read; i++) {
                    //     printf("%02x", buffer[i]);
                    // }
                }
                fclose(f);
                remove("clear_encrypt");
                // remove("cipher_encrypt");
            } else {
                fprintf(stderr, "Wrong number of arguments");
                return 1;
            }
            printf("\nEncrypted. Written %d bytes of data\n", bytes_written);
            return 0;
            break;
        case 'd':
            if (argc == 4) {
                get_password(s);
                // Works, with exception of broken padding at the end
                // of aoutput file.
                bytes_written = decrypt_it(argv[2], argv[3], s);
            // TODO
            } else if (argc == 3) {
                get_password(s);
                char *cli = argv[2];
                // unsigned char hex_string[strlen(cli) + 1];
                // memcpy(hex_string, cli, sizeof(hex_string));
                // unsigned char binary_data[strlen((char *)hex_string) / 2];
                // for (int i = 0; i < sizeof(binary_data); i++) {
                //     sscanf((char *)hex_string + 2 * i, "%2hhx", &binary_data[i]);
                // }
                // unsigned char binary_data[strlen(cli)/2];
                // hex2bin(binary_data, cli, strlen(cli));
                // OPENSSL_hexstr2buf_ex(binary_data, sizeof binary_data, NULL, cli, '\0');
                char command[1024];
                sprintf(command, "perl -e 'print pack(\"H*\", \"%s\")' > cipher_decrypt", cli);
                system(command);
                FILE *f;
                // f = fopen("cipher_decrypt", "wb");
                // fwrite(binary_data, sizeof(char), sizeof(binary_data), f);
                // fclose(f);
                bytes_written = decrypt_it("cipher_decrypt", "output_decrypt", s);
                f = fopen("output_decrypt", "r");
                unsigned char buffer[BUFSIZ];
                size_t bytes_read;
                while ((bytes_read = fread(buffer, 1, sizeof buffer, f)) > 0) {
                    for (int i = 0; i < bytes_read; i++) {
                        printf("%c", buffer[i]);
                    }
                }
                fclose(f);
                // remove("cipher_decrypt");
                // remove("output_decrypt");
            } else {
                fprintf(stderr, "Wrong number of arguments");
                return 1;
            }
            printf("Decrypted. Written %d bytes of data\n", bytes_written);
            return 0;
            break;
        case '?':
            print_help(argv[0]);
            return 0;
            break;
        default:
            print_help(argv[0]);
            return 0;
            break;
        }
    }

    print_help(argv[0]);

    return 0;
}

// simple function to print some help when needed with
// name of the command line calling program set as the
// beginning of output
void print_help(char *argv) {
    printf("Usage:\n");
    printf("%s [-e(ncrypt) / -d(ecrypt)] [file in] [file out]\n", argv);
    printf("or\n");
    printf("%s [-e(ncrypt) / -d(ecrypt)] [text]\n", argv);
}

// didn't check on Windows
// right now it return hardcoded password so
// development is a lot faster
// remove `s = "123.."` line to make interactive
// password prompt
// uncomment `scanf("%s", s)`;` to get the password from
// command line
// `system(stty -echo)` ensure that password is not visible
void get_password(char *s) {
    #ifdef _WIN64
        #include <conio.h>
        int i=0;
        printf("Password (32 characters): ");
        while(1){
            s[i]=_getch();
            if(s[i]=='\r'){
                s[i]='\0';
                break;
            }
            i++;
        }
        printf("\n");
    #else
        printf("Password (32 characters): ");
        // hide password
        system("stty -echo");
        // for (int i = 0; i < 32; i++) {
        //     s[i] = 8 % i;
        // }
        // default
        s = "12345678123456781234567812345678";
        // uncomment to get input
        // scanf("%s",s); // Won't echo to screen while being typed
        printf("%s", s);
        // make another input calls visible
        system("stty echo");
        printf("\n"); // Don't print out password
    #endif
}
```

## My favorite part of it all was this small Makefile

```makefile
SOURCES = nutek-ccrypt.c
OBJECTS = $(SOURCES:.c=.o)
CFLAGS = -Wall -lssl -lcrypto -I/usr/local/opt/openssl/include -L/usr/local/opt/openssl/lib
DEBUG = -g

all: nutek-ccrypt

nutek-ccrypt: $(OBJECTS)
    clang $(CFLAGS) $(DEBUG) $(OBJECTS) -o nutek-ccrypt
    # rm nutek-ccrypt.o

%.o: %.c
    clang $(DEBUG) -c $< -o $@

clean:
    rm -f nutek-ccrypt $(OBJECTS)
```

Here I learned how to create simple build script than can clean after itself
and build a program for myself. I don't have a girlfriend to send this
**I love you** so `C` - 💔. Watch out for those low level buffers... I
already hate them, just like _JavaScript_ **Promise**.

## Example poem

```text
Man and woman, two halves of a whole,
Together they stand, strong and bold.

Man, with his strength and steady hand,
A protector, a leader, a true friend.

Woman, with her grace and gentle touch,
A nurturer, a guide, a loving crutch.

Together they balance, yin and yang,
Complementing each other, in all they do and say.

Man and woman, a perfect pair,
Together they soar, without a care.

Through joy and sorrow, they stand tall,
For in each other, they have it all.

Man and woman, a love so true,
Forever bound, in all they do.

Together they create, a world so bright,
Filled with love, hope, and light.

So let us honor and cherish, the bond between man and woman,
For in their unity, lies the strength of all human.
```

## Pull request welcomed

Tell me what I did wrong, and how I can improve. This can be only `C`, or any other smart way to do this. **PLEASE HELP ME SOLVE THIS** 🧩 [source code](https://github.com/nutek-terminal/nutek-terminal.github.io)

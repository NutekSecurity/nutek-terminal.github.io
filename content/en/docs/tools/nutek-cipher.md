---
title: "Nutek Cipher"
description: "Encrypt and decrypt files and text from terminal using Nutek Cipher."
lead: "🔐 Encrypt and 🔑 decrypt files and text from terminal using Nutek Cipher."
date: 2023-08-09T00:15:31+02:00
lastmod: 2023-08-09T00:15:31+02:00
draft: false
images: []
menu:
  docs:
    parent: ""
    identifier: "nutek-cipher-74b729a1021691dc7a4fbf1ed59f1a75"
weight: 999
toc: true
---

<img src="https://img.shields.io/crates/v/nutek-cipher.svg" alt="Crates.io">

<img src="https://img.shields.io/badge/license-MIT-violet.svg" alt="MIT License">

## Why?

Since ancient times people have been using ciphers to protect their secrets.
I think even animals have their own way of communicating with each other
without letting others know what they are talking about.

## Installation

```shell
cargo install nutek-cipher
```

or download the binary for your OS from [releases](https://github.com/nutek-terminal/nutek-cipher/releases) - Windows, Linux, MacOS

## Usage

```shell
nutek-cipher --help
```

Display help message.

```text
Usage: nutek-cipher [OPTIONS]

Options:
  -e, --encrypt                        encrypt
  -d, --decrypt                        decrypt
  -i, --input <INPUT>                  set input file
  -o, --output <OUTPUT>                set output file
      --key-file <KEY_FILE>            key from file
      --nonce-file <NONCE_FILE>        nonce from file
      --stdout                         print results to stdout
  -h, --help                           print help
  -V, --version                        print version
```

## Examples

> You have to provide 32 characters (bytes) long key and 12 characters (bytes)
long nonce. You can provide them from file or from stdin during program
execution.

### Encrypt file

```shell
nutek-cipher -e -i file.txt -o file.txt.enc
```

### Decrypt file

```shell
nutek-cipher -d -i file.txt.enc -o file.txt
```

### Encrypt text

```shell
echo "I ❤️ you" | nutek-cipher -e --stdout
```

### Decrypt text

```shell
echo "_your_encrypted_content_" | nutek-cipher -d --stdout
```
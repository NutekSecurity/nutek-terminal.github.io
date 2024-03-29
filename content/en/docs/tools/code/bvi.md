---
title: "Bvi"
description: ""
lead: ""
date: 2023-02-16T08:49:21+01:00
lastmod: 2023-02-16T08:49:21+01:00
draft: false
images: []
menu:
  docs:
    parent: "code"
    identifier: "bvi-0134e9baa0905ec1d3933f8903cf5328"
weight: 999
toc: true
---


## Description

bvi is a binary file editor.

## Installation

```bash
brew install bvi
```

## Usage

```bash
bvi /path/to/file
```

## Resources

- [bvi](http://bvi.sourceforge.net/)
- [bvi User Guide](http://bvi.sourceforge.net/doc/bvi.html)
- [bvi API](http://bvi.sourceforge.net/doc/bvi.html)

## Similar

- vim
- vi
- ed
- ex
- nano
- pico
- joe
- micro

## help

```text
BVI(1)                                                 User Commands                                             BVI(1)

NAME
       bvi, bview - visual editor for binary files

VERSION
       bvi-1.4.1

SYNOPSIS
       bvi   [-R] [-c cmd] [-f script] [-s skip] [-e end] [-n length] file...  bview [-R] [-c cmd] [-f script] [-s skip] [-e end] [-n length] file...

OPTIONS
       file...
       A  list  of    filenames.  The first one will be the current file and will be read into  the  buffer.    The  cursor  will  be  positioned on the first line of the buffer.  You can get to the
       other files with the ":next" command.

       -R  "Readonly": The readonly flag is set for all the files, preventing accidental overwriting with a write command.

       -s skip
       causes bvi to load a file not from the start but from offset skip.  Skip offset bytes from the beginning of the input.  By default, offset is interpreted as a decimal number.  With a
       leading 0x or 0X, offset is interpreted as a hexadecimal number, otherwise, with a leading 0, offset is interpreted as an octal number.  Appending the character b, k, or m to offset causes
       it to be interpreted as a multiple of 512, 1024, or 1048576, respectively.

       -e end
       causes bvi to load a file not till end but till address end.

       -n length
       causes bvi not to load the complete file but only length bytes.

       -c cmd
       cmd will be    executed  after     the  first file  has been read. If the     cmd  contains spaces  it  must     be enclosed in double quotes (this depends on    the  shell  that  is  used).

       -f script
       This command provides a means for collecting a series of "ex" (colon) commands into a script file, then using this file to edit other files. Since there is no binary stream editor "bsed",
       you can use this option to make several global changes in a binary file.

DESCRIPTION
       Bvi stands for "Binary VIsual editor".  Bvi is a screen oriented editor for binary files; its command set is based on that of the vi(1) text editor.  As bvi is a binary editor, it does not
       have the concept of "lines".  All end-of-lines (EOLs) are simply bytes.    Therefore bvi's commands are different from vi's commands for all line-oriented commands (see below).

COMPARISON
       The main differences between Vi and Bvi are:

       The screen is divided in three sections or panes: The byte offset (extreme left), the hex pane (middle), and an ascii pane (right) which shows as printable characters those bytes in the hex
       pane.  On an 80 column terminal there will be sixteen hex values and their ASCII values on each screen line.  Note that (as one would expect) the first byte has the offset '0' (zero).

       You can toggle between the hex and ascii windows with the tab key (TAB).     Toggling between these two windows does not change the current position (offset) within the file.

       No "lines" concept: Files are treated as one long stream of bytes.  The characters "newline" and "carriage return" are not special, id est they never mark the end of lines.  Therefore the
       lines on the screen do not represent lines in the usual way.  Data is broken across screen lines arbitarily.  As a consequence there are no commands in bvi from ex or vi that are based on line
       numbers, eg "dd", "yy", 'C', 'S', 'o', 'O'.  This also changes the meaning of "range" before the ":write" command to a byte offset, ie the command ":100,200w foo" writes all *bytes* (not
       lines) from offset 100 to offset 200 to the file "foo".

       No "text objects": There are also no text-specific arrangements like words, paragraphs, sentences, sections and so on.

       Extended "ruler": The bottom line of the screen shows the current address (byte offset) and the current character in these notations:

           octal, hexadecimal, decimal and ascii.

       Search patterns: All search commands understand these special characters:

        .     any character
        []     set of characters
        *     zero or more occurrences of previous char or set

       But as there is no concept of lines you cannot use the standard symbols ("anchors") for "begin-of-line" ('^') and "end-of-line" ('$').  Searching for the start/end of lines must be done
       explicitly by adding these special characters to your search pattern using these meta sequences:

           \n   newline
           \r   return
           \t   tab
           \0   binary zero

       Additional search commands: Similar to the text search commands there are additional hex-search functions '\' and '#' which allow to search for any byte value.    Example:  "\62 76 69" will
       search for the string "bvi".  Spaces between hex value are optional, so searching for "6775636B6573" will find "guckes".

       Changing the length of data (insertion, deletion) moves the data to other addresses; this is bad for many cases (eg. databases, program files) and is thus disabled by default. You can enable
       this commands by typing

        :set memmove

       BVI Modes:

       Command Mode (Normal Mode):

       Input is treated as command.  Note that command mode is the default mode after startup and after escaping from input mode.  Use ESC (escape) to cancel a partial (uncompleted) command.

       Input Mode:

       Input is treated as replacement of current characters or (after the end of the file) is appended to the current file.  This mode is entered from command mode by typing one of 'i', 'I', 'A',
       'r', or 'R'.  You can enter the characters from the keyboard (in the ASCII window) or hexadecimal values (in the HEX window).  Type TAB to switch between these two windows.  Type ESC to finish
       the current input and return to command mode.  Type CTRL-C to cancel current command abnormally.

       Command line mode (Last Line Mode or : mode):

       Similar to vi, this mode is entered by typing one of the characters : / ? \ # !    The command is terminated and executed by typing a carriage return; to cancel a partially typed command, type
       ESC to cancel the current command and return to command mode.

ENVIRONMENT
       The editor recognizes the environment variable BVIINIT as  a command  (or  list of commands) to run when it starts up. If this variable is undefined, the editor     checks     for  startup commands
       in  the    file  ~/.bvirc    file, which you must own.  However, if there is a .bvirc owned by you  in  the    current directory,  the     editor takes its startup commands from this file - overriding
       both the file in your home  directory  and the environment variable.

TERMINOLOGY
       Characters names are abbreviated as follows:
        Abbr.     ASCII    name      aka
        CR          010    carriage return
        ^A          001    control-a
        ^H          008    control-h
        ^I          009    control-i      aka TAB
        ^U          021    control-u
        ^Z          026    control-z
        ESC          027    escape           aka ESC
        DEL          127    delete
        LEFT      ---    left  arrow
        RIGHT     ---    right arrow
        DOWN      ---    down  arrow
        UP          ---    up    arrow

COMMAND SUMMARY
       See the TERMINOLOGY for a summary on key name abbreviations used within the following description of commands.

       Abstract:
     Arrow keys move the cursor on the screen within the current window.

       Sample commands:
     :version    show version info
     <- v ^ ->   arrow keys move the cursor
     h j k l     same as arrow keys
     u         undo previous change
     ZZ         exit bvi, saving changes
     :q!         quit, discarding changes
     /text         search for text
     ^U ^D         scroll up or down

       Counts before bvi commands:
     Numbers may be typed as a prefix to some commands.
     They are interpreted in one of these ways.

     screen column         ⎪
     byte of file         G
     scroll amount         ^D     ^U
     repeat effect         most of the rest

       Interrupting, canceling
     ESC         end insert or incomplete command
     DEL         (delete or rubout) interrupts

       File manipulation:
     ZZ         if file modified, write and exit;
             otherwise, exit
     :w         write changed buffer to file
     :w!         write changed buffer to file, overriding
             read-only ("forced" write)
     :q         quit when no changes have been made
     :q!         quit and discard all changes
     :e file     edit file
     :e!         re-read current file, discard all changes
     :e #         edit the alternate file
     :e! #         edit the alternate file, discard changes
     :w  file    write current buffer to file
     :w! file    write current buffer to file overriding
             read-only (this "overwrites" the file)
     :sh         run the command as set with option "shell",
             then return
     :!cmd         run the command cmd from "shell", then
             return
     :n         edit next file in the argument list
     :f         show current filename, modified flag,
             current byte offset, and percentage of
             current position within buffer
     ^G         same as :f

       Additional edit commands
     You can insert/append/change bytes in ASCII/binary/decimal/ hexadecimal or octal representation. You can enter several (screen) lines of input. A line with only a period (.) in it will
       terminate the command. You must not type in values greater than a byte value. This causes an abandonment of the command.     Pressing the CR key does not insert a newline - character into the
       file. If you use ASCII mode you can use the special characters \n, \r, \t and \0.

     :i aCR         insert bytes (ASCII) at cursor position
     :a bCR         append bytes (Binary) at end of file
     :c hCR         change bytes (hexadecimal) at cursor position

       Bit-level operations
     :and n         bitwise 'and' operation with value n
     :or  n         bitwise 'or' operation with value n
     :xor n         bitwise 'xor' operation with value n
     :neg         two's   complement
     :not         logical negation
     :sl i         shift  each byte i bits to the left
     :sr i         shift  each byte i bits to the right
     :rl i         rotate each byte i bits to the left
     :rr i         rotate each byte i bits to the right

       Command mode addresses
     :w foo        write current buffer to a file
            named "foo"
     :5,10w foo    copy byte 5 through 100 into as
            file named foo
     :.,.+20w foo    copy the current byte and the next
            20 bytes to foo
     :^,'aw foo    write all bytes from the beginning
            through marker 'a'
     :/pat/,$ foo    search pattern pat and and copy
            through end of file

       Positioning within file:
     ^B     backward screen
     ^F     forward  screen
     ^D     scroll down half screen
     ^U     scroll up   half screen
     nG     go to the specified character
         (end default), where n is a decimal address
     /pat     next line matching pat
     ?pat     previous line matching pat
     \hex     jump to next      occurrence of hex string hex
     #hex     jump to previous occurrence of hex string hex
     n     repeat last search command
     N     repeat last search command, but in opposite
         direction

       Adjusting the screen:
     ^L     clear and redraw screen
     zCR     redraw screen with current line at top of screen
     z-     redraw screen with current line at bottom of
         screen
     z.     redraw screen with current line at center of
         screen
     /pat/z- search for pattern pat and then move currents
         line to bottom
     ^E     scroll screen down 1 line
     ^Y     scroll screen up   1 line

       Marking and returning:
     mx     mark current position with lower-case letter x
         Note: this command works for all lower-case letters
     'x     move cursor to mark x in ASCII section
     `x     move cursor to mark x in HEX section
     ''     move cursor to previous context in ASCII section
     ``     move cursor to previous context in HEX section

       Line positioning:
     H         jump to first    line on screen ("top")
     L         jump to last    line on screen ("low")
     M         jump to middle    line on screen ("middle")
     -         jump onto previous line on screen
     +         jump onto next    line on screen
     CR         same as +
     DOWN or j   next     line, same column
     UP   or k   previous line, same column

       Character positioning:
     ^         first byte in HEX window
     $         end of screen line
     l or RIGHT  jump onto next byte (within current
             screen line)
     h or LEFT   jump onto previous byte (within current
             screen line)
     ^H         same as LEFT
     space         same as RIGHT
     fx         find next       occurrence of character x
     Fx         find previous occurrence of character x
     n⎪         jump onto nth byte/character within current
             line

       Strings:
     (works similar to the strings(1) command)
     Note:    "Words" are defined as strings of "nonprinting
     characters".
     e     jump to next      end    of word
     w     jump to next      begin of word
     b     jump to previous begin of word
     W     forward to next string delimited with a
         \0 or \n
     B     back to previous string delimited with a
         nonprinting char

       Corrections during insert:
     ^H     erase last character (backspace)
     erase     your erase character, same as ^H (backspace)
     ESC     ends insertion, back to command mode

       Append and replace:
     A     append at end of file
     rx     replace current bte with char 'x'
     R     enter replace mode; for all subsequent input,
         the current byte is overwritten with the next           input character; leave replace mode with ESC.

       Miscellaneous Operations:
     TAB     toggle between ASCII and HEX section

       Yank and Put:
     3ySPACE yank 3 characters
     p     insert contents of yank buffer
     o     replace text with content of yank buffer
     P     put back at end of file

       Undo, Redo:
     u     undo last change
         Note:    Only the last change can be undone.
         Therefore this commands toggles between the
         last and second-t-last state of the buffer.

       Setting Options:
     With the :set command you can set options in bvi

     Option        Default  Description

     autowrite  noaw     Save current file, if modified, if you
                 give a :n, :r or ! command
     columns    cm=16    on an 80 character wide terminal
     ignorecase noic     Ignores letter case in searching
     magic        nomagic  Makes . [ * special in patterns
     memmove    nomm     enables insert and delete commands
     offset        of=0     adds an offset to the diplayed addresses
     readonly   noro     If set, write fails unless you use ! after command
     reverse    nore     display otherwise-printable characters with their
                 high bit set as reverse video
     scroll        sc=1/2 window
                 Number of lines scrolled by ^U and ^D
     showmode   mo         Displays statusline on bottom of the screen
     terse        noterse  Let you obtain shorter error messages
     window        window=screensize
                 Lines in window, can be reduced at slow terminals
     wordlength wl=4     Length of an ASCII-string found by w, W, b or B
     wrapscan   ws         Searches wrap around past the end of the file
     unixstyle  nous     The representation of ascii characters below
                 32 is displayed in the statusline as shown
                 in ascii(7) if unset rather in DOS-style (^A)

AUTHOR
       bvi was developed by Gerhard Buergmann, Vienna, Austria gerhard@puon.at

WWW
       Bvi Homepage:  http://bvi.sourceforge.net/ Vi Pages:     http://www.guckes.net/vi/clones.php3             (all about Vi and its clones)

FILES
    $HOME/.bvirc          editor startup file   ./.bvirc          editor startup file

BUGS
       Bvi does not update the screen when the terminal changes its size.

SEE ALSO
       bmore(1), vi(1), strings(1), ascii(5)

3rd Berkeley Distribution                                   BVI Version 1.4.1                                             BVI(1)
```bash

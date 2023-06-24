---
title: "Python & Neovim"
description: "Basic Python3 and Neovim usage example."
lead: "Basic Python3 and Neovim usage example."
date: 2022-09-02T19:37:24+02:00
lastmod: 2022-09-02T19:37:24+02:00
draft: false
menu:
  docs:
    parent: "tools"
weight: 110
toc: true
---

 language & text editor

## What do you need to have?

*Hej*, today we begin learning with __Nutek__ to be able to use it
how I see it fit. First be sure you have one of the following:

* `neosb/nutek-core:0.4.0` from [Docker Hub](https://hub.docker.com/r/neosb/nutek-core)
* `Nutek` from [crates.io](https://crates.io/crates/nutek) or [Github](https://github.com/phoenix-journey/nutek/releases) - working on a fix
* You could follow on with `Python3`, `pip`, `venv` and `Neovim`

## What you will learn?

I want to show you few `Python` use cases and how to write code in
`Neovim`. We will use this in future lessons and hacking activities
that will surely come to us as we go.

I'm not the only source of truth you should rely on, so try to
[bing-search](https://crates.io/crates/bing-search) (which is the part
of Nutek) or use [Google](https://www.google.com) to look-up
interesting parts and to broaden your knowledge.

## Where to look for answers?

I give you some links that might help you in the beginning.

`Neovim` is compatible version of `Vim` which is `Vi` improved,
it's one of the basic text editor found on most of the UNIX-like
operating systems, thus knowing how to use it is likely to payoff
int the future :)

* [Neovim documentation](https://neovim.io/doc/)
* [Vim cheatsheet](https://devhints.io/vim)
* [Vim cheatsheet #2](https://vim.rtorr.com/)
* [Vim tutorial](https://danielmiessler.com/study/vim/)
* open `nvim` in terminal and type `:Tutor` to open one of the first
interactive tutorials out there that will teach you the basics of
Neovim.
* [Vim Plug](https://github.com/junegunn/vim-plug) minimalist plugin manager
* [Awesome Vim plugins](https://vimawesome.com/)

`Python` one of the most used programming languages, also one of
the easiest to learn. So without bothering you with developers
jargon...

* [Documentation](https://docs.python.org/3/)
* [Tutorial](https://docs.python.org/3/tutorial/index.html)
* [PyPI - pip installable packages](https://pypi.org/)

## 3.. 2.. 1.. 🚀

First of all, to start `Neovim` type `nvim` in your terminal, or
if you are ready to edit a text file, type
`nvim my_first_python_script.py`. `.py` extension tells `nvim`
that it's a Python file and if you use `Nutek` or `nutek-core`, after
first start you will be given a chance to install `coc-jedi` which
helps a lot with `Python` files. Keep pressing `<Enter>` untill it's
done. I have preinstalled there, for you too,
[Github Copilot](https://github.com/features/copilot), so just.

```vim
:Copilot setup
```

inside `Neovim`, confirm your credentials on `Github`, and have a
helping hand ready to assist you with AI generated snippets of code.

Now. To make the first script a little bit challenging, let's use the
`my_first_python_script.py` `nvim` window and write as follows.

```vim
:tabnew
:terminal
<i>
python3 -c "print('Hej piękna!')"<Enter>
```

In context of Vi, Vim and Neovim `<i>` means pressing the `i` keyboard
key. There is a lot about text in operating systems, especially
`UNIX`-es, where every part of the operating system is a text file and
`Windows` sometimes even borrows the thinking, e.g. `/etc/hosts/` file.
To the `UNIX` system family belongs `Linux` flavours like `Debian`, `Ubuntu`, `Mint`, `Arch`, `Fedora`, `openSUSE`,
`Red Hat Enterprise Linux`; `macOS`, `BSD` based systems, `freeBSD`,
`openBSD`. For now we won't be learning how to cope with OS, right now
we want to write something, then we might know how to do something with
operating system in terminal and in scripts.

Back on track. You should see now a response from your terminal saying
to you `Hello beauty` in *Polish*. We used `python3` and a switch `-c`
which tells Python to run the code in between quotes. This is called
an `inline` script. Now please press:

```vim
<C-\>
<C-n>
```

It will exit terminal mode and let you operate Neovim normally. It's `Ctrl+backslash` and `Ctrl+n`.

Right now I want you to get to previos tab.

```vim
:tabprevious
```

You might also autocomplete the statement with a `<tab>`, or use mouse
to switch tabs, if have one, but mouse support depends on your
configurations, and we want to stay focused, so using only keyboard
might really help you stay as creative as it can be. Now type the
comment after `#` sing and if you use Github Copilot, when you press
`<Enter>` and wait a second or two, you should get a proposition to
autocomplete the print statement. Agree with `<tab>`, dismiss with
`<ctrl-]>`, and search for other suggestion with `<alt-]>`.

```python
 hacking rules!<Enter>
print("Hacking Rules!")
```

You have your first script in text file. So save it. First get out of
insert mode with `<Esc>` to get to normal mode, then please type.

```vim
:write
```

I want to run it in a window, which will be visible in this tab, to do
it follow on with this commands which will close all the other tabs,
split window horizontally, switch to other window, open terminal,
run your script and exit Neovim.

```vim
:tabonly
<C-w+s>
<C-w+j>
:terminal
<i>
python3 my_first_python_script.py
<Enter>
<C-\>
<C-n>
:q
:wqa
```

You should know now what is the coolest computer activity 🥷.

## What we learned so far?

### Neovim

* how to open a text file (`nvim filename`)
* how to create new tab (`:tabnew`)
* how to open the terminal (`:terminal`), get into insert mode (`<i>`),
execute inline Python script (`-c "python code here"`) and exit the
terminal insert mode (`<C-\><C-n>`)
* how to write text (`<i>`), exit from insert mode (`<Esc>`) and write
changes to file (`:write`)
* close all the other tabs (`:tabonly`)
* split window horizontally (`<C-w+s>`) or vertically (`<C-w+v>`) and
go to other windows (`<C-w+h/j/k/l>`) - where `h` is left, `j` is down,
`k` is up, and `l` is left and it works with moving around the text in
normal and visual mode
* close tab, window, or just exit Neovim (`:q`)

### Python

* how comment looks like (`# text that is not a code after pound sign`)
* how to output text to terminal (`print("this will be the output"`)

### Copilot 👩🏻‍💻

* he know what do you mean if you provide enough clues, like a comment
imported modules, docstring, class name, variables, method or any
other part of meta that is an input for an AI generated "guess"
* accept suggestion with `<tab>`
* ask for next suggestion with `<alt-]>`
* dismiss suggestion with `<ctrl-]>`

## Flying higher

Open new file.

```shell
nvim learning_to_fly.py
```

And write a comment

```python
 that prints number from 16 to 0.
 number is divisible by 4 display 💣.
 loop finish print 💥
```

Press `<Enter>`, write `f`, wait for suggestion, press `tab` to
accept, `<Enter>` once more, `<tab>` to accept, `<Enter>` and `<tab>`
again. You should have now fully functional script that does
exactly what it's asked to do. You should have to have Copilot
setup to be able to do this. Exit insert mode with `<Esc>` and
write the file with `:write`. If you're using `Nutek`, open
new bash sessions with `nutek`, or if you're using only Docker,
run `docker exec -it name-of-your-container bash`. I mean, that
you need other terminal window where you can access the file
we're working on right now.

```shell
python3 learning_to_fly.py
```

## What you learned from this script?

### For loop

In one form of it, for loop runs for the exectly specified times
code which is after the colon sign. Next lines are indented, and will be exucuted. You can ask to skip one iteration with `continue`, exit
loop with `break` wich will resume code flow of unindented lines. It
also saves a variable `i` which is the current value of the loop.

```python
for i in "don't go to school, become ninja!":
    if i == "!":
        print("🥷")
```

As you can see, the value of variable can be in many forms too.

### If, elif and else statement

Check if condition is true. Uses boolean logic to check if code after
colon can be run. It can be `True` or `False`. If the condition doesn't
stands, goes to next `elif` check, or straight to `else`. Both are
optional, but there can be many `elif` checks, but one `else`
statement.

```python
if True == False:
    # this will never run
    pass
elif not True == True:
    # this will never run
    pass
elif False == (not False):
    # this will never run
    pass
else:
    # this will run because it does not check for condition \
    # only if it is the last checked statement \
    # if one of the if, or elif will run, after the end of \
    # indentation the program flow will resume after the whole \
    # if check
    print("This is my last resort")
```

There are also other methods to use `if` statements. With `and` clause
or `or` clause. Let me show you.

### And

```python
if True and False:
    # this will never run
    pass
elif True and True and False:
    # this will never run
    pass
elif False and False:
    # this will never run
    pass
elif True and True:
    print("We've got a winner!")
```

### Or

```python
if True or False:
    # this will run
    print("Hmmm... Why we do this?")

if True or True:
    # this is another check that will run
    print("Simply the best")

if False or False:
    # this will never run
    pass
```

To say it's kind of *magic* is not enough. `and` check is `True` only
if all of the parts of equation are `True`, but `or` clause let you
pass if check when only one part is `True`. You can help yourself
with parentheses (`True and (False or True)`).

### Range function

Functions are parts of code that can be run many times saving you
typing, so you dont write `Hello world` and `Hello Agnes` two times
but instead you define a function and then substitue arguments
in your source code as variables that help you save time. It's like
cooking. You could add two spoons of sugar, but one spoon of flour.

```python
def hello(who):
    """
    friendly greeting
    arguments:
    who (str): who to greet
    returns:
    greeting (str): friendly greeting
    """
    greeting = "Hello " + who + "! How are you?"
    return greeting
hello("Agnes")
hello("Asia")
```

You learned that `range` function takes 3 arguments, with optional
step and is invoked using parentheses, `range(0, 16)`. Check that with
hovering over the name of method (aka function) and pressing `<K>`.
You can see that when hovering over your `hello` function and again
pressing `<K>`, you can read what is called __dockstring__, think
about it as helping me understand what do you wanted from me, or how
it should run exactly. Then use Copilot.

To invoke hello function, use `hello("world")`

### List

`range(0, 4)` is the same as a list of four items, starting with 0 -
`[0, 1, 2, 3]` to access/select an item in a list you use brackets
`[x]`. So the first element is `[0]` and last is `[-1]` or in our
case `[3]`.

### Variable

We have also asigned a number to variable, and a character to variable.
Variable is a placeholder for your values, that let's you use stored
value in other parts of your program. Variables can be `numbers`,
`strings`, `results` of your calculations, `methods`, `classes`,
`lists`, `dictionaries` aka `hashmaps`, `tuples` - simply put,
`objects` and `basic data types`. Check for `type` of your data.

```python
data_type = type("this is str class")
print(data_type)
```

You should know that you will be using this a lot if you want to
make programs and scripts.

## Get request

First of all, be sure that you have `pip` and `venv` installed.
Now we will make a virtual environment for the next script to run.
Venv is used to *package* the program so it can be easily portable
and decoupled from other Python scripts. You might want to have
one package installed, or ten, but you don't need them in all of your
scripts, so you make a `virtual environment` with `venv` and safely
install what you need now and safely remove later.

```shell
mkdir my_first_get_request
cd my_first_get_request
python3 -m venv get_request
source get_request/bin/activate
python3 -m pip install requests
```

First you created a directory called `my_first_get_request`, then
you moved the current working directory to it, then created
virtual environment called `get_request` and activated it, then
installed requests package only for this environment.

Exit from previous Neovim session if you haven't already, and be sure
to first activate newly created Python environment and again run
`nvim my_get_request.py`

First of all we start with a bad request, which will give us some
intuition how the http protocol works.

```python
import requests
import json

 a bad get request to httpbin.org then show the error message \
 print the headers.
response = requests.get("http://httpbin.org/status/404")
print(response.status_code)
print(response.reason)
print(response.headers)
```

Then try again with another get request, that will send back some data.

```python
 a get request to httpbin.org/get with some parameters.
response = requests.get("http://httpbin.org/get",
        params={"name": "Szymon", "age": 34}
    )
print(response.status_code)
print(response.reason)
 the query string from the url.
query_string = response.url
print(query_string)
 the json data from the response.
data = response.json()
 print json data.
print(json.dumps(data, indent=4, sort_keys=True))
```

Here we see a classic example of getting data from an API. We provide
parameters, `name` and `age`, this would be likely a query to database.
In an `origin` header key, you can see value of your IP address,
you should know that it's always known, unless you are connected to
proxy like `TOR` or other kind of `VPN` that could route your request.

Change request to something else.

```python
response = requests.get("http://httpbin.org/get",
        params={"name": "John", "surname": "Dillinger"},
        headers={"Accept": "application/json"}
    )
```

You have encoded your first `json` request! JSON, stands for JavaScript
Object Notation which is very common format of exchanging data between
services. Most of the API's made to be available on the web support it.

So far you've learned how to get data from API, what about making a
class that will be an actual object of human cosmic conquer? But first
let's get some hands dirty with more Neovim commands. We need fuel
for our rocket science 🚀

## Working with files

:edit .

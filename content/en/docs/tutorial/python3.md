---
title: "Python3. Filling the Tank"
description: "Orbiting Earth with International Space Station using Python."
lead: "Orbiting Earth with International Space Station using Python."
date: 2022-09-09T14:28:32+02:00
lastmod: 2022-09-09T14:28:32+02:00
draft: false
menu:
  docs:
    parent: "tools"
weight: 130
toc: true
---

 ⛽️ for our rocket 🚀

## Ground-up

In [previous post]({{< ref "/docs/tutorial/python-neovim" >}})
I tried to show you how to write simple program in _neovim_ and
run using **python3**. Today I want to fill in the gaps in
your knowledge of my understanding of how developer work. First
of all we will touch on some Vim commands that migh be useful
and then we'll build a tool that show where International
Space Station is and who is currently in space. Maybe we will
call an Uber for them later, right now they have to use their scooters.

Let's start with

```shell
nvim round_globe.py
```

## Nvim

Then please feel free to skip to the [next section](#python-class)
if you already feel comfortable with `nvim`. I want to elaborate a
little bit on the subject.

So you probably want to know how to _copy & paste_? My solution:

```vim
<v>
" use arrow keys or h,j,k,l to highlight and...
<y>
" place cursor in the place where you want to paste and...
<P>
```

Do you want to reorganize your codebase and move lines around?

```vim
<V>
" highlight
<x>
" cursor in the place and...
<p>
```

To undo last step, use `<u>` and `<C-r>` to redo.

You can open more than one file, in separate window or tab. I show
you the tab option here.

```vim
:tabedit i_swear_i_rockyou.py
" switch to previous tab
:tabprevious
" then to close a tab and all it's windows (you know you can
" use <tab> key to autocomplete?)
:tabclose
```

I hope it helps.

### Helpful Vim links

Once more, I encourage you to explore on theese cheatsheets and
experiment in your terminal window, tab or webshell.

* [devhints.io](https://devhints.io/vim)
* [rtorr.com](https://vim.rtorr.com/)

**If** you use some flavour of `Nutek`, you can simply try this out
in your terminal.

```shell
w3m https://devhints.io/vim

w3m https://vim.rtorr.com/
```

I will teach you more about `w3m` later on, but to quit it - simply
`<q><y>`

## Enough is enough

If you can't stand the pace, or my attitude, or simply want to
explore... Here's an email from [freecCodeCamp](https://freecodecamp.org) where the subject is **JavaScript**.

```text
Quincy Larson <quincy@freecodecamp.org>
6:11 AM (9 hours ago)
to me

Here are this week's five links that are worth your time:

1. Learn React for Beginners. This new freeCodeCamp Front-End JavaScript course will teach you all about React Hooks, State, the Context API, and more. You'll code along with three experienced software engineers, building projects step-by-step. (8 hour YouTube course): https://www.freecodecamp.org/news/learn-react-from-three-all-star-instructors/

2. And if you'd prefer to learn Angular, I'm thrilled to share this course with you as well: Learn Angular and TypeScript for Beginners. This in-depth course will teach you TypeScript Data Types, Angular Directives, Components, RxJS, and Lifecycle Hooks. (18 hour YouTube course): https://www.freecodecamp.org/news/angular-for-beginners-course/

(...)
```

## Python class

It's not that you're my student. It's just object oriented
programming concept. Most, if not all, python types are object
and you can create your own types, classes, too. Create your
environment and I show you how to call from Houston to space.

```shell
 case you forgot how to prepare your environment, here's how
python3 -m venv space_station
source space_station/bin/activate
 you see now?
(space_station)% python -m pip install requests
 the (space_station)% part, as it is only for reference
```

### Import

It's time for the show to begin. Clear out your `round_globe.py`
file (you might need to put it in the same directory as your
environment). Starting simple, `import` statements. We will use
`json` and `requests` libraries. Put them in separate lines.

```python
 statemnts. What we will use.
import requests
import json
```

### ISS

Now we go big. Whole class. ISS - International Space Station. It is
initialized without any arguments, then proceeds with a get request
to an external _api_ resource. `API`s are services on the Internet that
perform actions and/or sends data. You can even create your own and
host for other well behaved users! I check for a `HTTP` status code
`200` - that means everything is `OK` and I **parse** the response
json data to `self.lat` and `self.lon` class instance variables. If
there is an error, we print out the status code and exit.

Then I make two methods `get_lat` and `get_lon` which return the stored
latitude and longitude ISS position variables. You can see here that
accessing instance variables, as well as functions must be prepended
with `self.`, but you are not limited to creating only such objects.
In `__init__` we can observe use of local variable `response` and
`status_code` which _dies_ out when out of scope and you can no
longer access them from other parts of code.

The last bit of information is `__str__(self)` method that when used
to print object, will returned stated action replacing `{}` with
subsequent values.

The last thing I want to say is about indentation, namely tabs, or
spaces, which must match the hierarchical pattern and be consistent.
Otherwise you might spend much more time debugging your application
than you should.

```python
 class definition
class ISS():
    # Class to represent the International Space Station
    # initialize the class
    def __init__(self):
        # get the ISS location data
        response = requests.get("http://api.open-notify.org/iss-now.json")
        status_code = response.status_code
        # if the response was successful, parse the JSON data
        if status_code == 200:
            response_json = response.json()
            self.lat = response_json['iss_position']['latitude']
            self.lon = response_json['iss_position']['longitude']
        # if the response was not successful, print the status code and exit
        else:
            print("Error: " + str(status_code))
            exit(1)

    # return self.lat, self.lon
    def get_lat(self):
        return self.lat
    def get_lon(self):
        return self.lon

    # pretty print the ISS location
    def __str__(self):
        return "ISS location: latitude: {}, longitude: {}" \
                .format(self.get_lat(), self.get_lon())
```

### Where we at now

To make the `round_globe` program much more exciting I introduce
another class that retrieves the Earth position of provided at
initialization attributes latitude and longitude. The concept
stays the same.

```python
 class definition
class PositionRelativeToEarth():
    # Initialize the class
    def __init__(self, latitude, longitude):
        # get the position data
        response = requests.get(
                "https://api.bigdatacloud.net/data/reverse-geocode-client?latitude={}&longitude={}" \
                        .format(latitude, longitude))
        status_code = response.status_code
        # if the response was successful, parse the JSON data
        if status_code == 200:
            response_json = response.json()
            self.country = response_json['countryName']
            self.countryCode = response_json['countryCode']
            self.city = response_json['locality']
        # if the response was not successful, print the status code and exit
        else:
            print("Error: " + str(status_code))
            exit(1)

    # pretty print position
    def __str__(self):
        return "Position: country: {}, countryCode: {}, city: {}" \
                .format(self.country, self.countryCode, self.city)
```

### Astronauts

I want to show you, that you are not limited to sequential program
structure, and you can store methods outside of classes too. This one
gets our heroes, astronauts in space and when the method is invoked
will print out this data to console.

```python
.get("http://api.open-notify.org/astros.json")
 is in space?
def astros():
    # make the request
    response = requests.get("http://api.open-notify.org/astros.json")
    status_code = response.status_code
    # if the response was successful, parse the JSON data
    if status_code == 200:
        data = response.json()
        # Get number of people in space.
        number = data["number"]
        print("Number of people in space: {}".format(number))
        people = data["people"]
        # Print people in space.
        print("People in space: ")
        for person in people:
            print(person["name"])
    # if the response was not successful, print the status code and exit
    else:
        print("Error: " + str(status_code))
        exit(1)
```

### Aggregate classes and methods

In this part of code I group all the bits provided before to contitute
a program that will run. I have to call the `astros()` function,
initialize `ISS` class and using another way of representing text data
`f"{1+1}"` clause I pretty print the Internationa Space Station
position relative to our globe, and at last I initilize
`PositionRelativeToEarth` with `__init__` attributes using iss
variable.

```python
 function
def main():
    astros()
    iss = ISS()
    print(f"{iss}")
    position = PositionRelativeToEarth(iss.lat, iss.lon)
    print(position)
```

### Run the script

The last part of code tells the `Python` interpreter to call `main`
function when file is run with `python` or `python3`.

```python
 main function only if this file is executed
if __name__ == '__main__':
    main()
```

That would be it for Today. Lookup where the International Space
Station is now and who is in the space when you please. You have me
now finished.

## Cleanup

### Deactivate

Deactivate command, will free you from Python's _virtual environment_

```shell
deactivate
```

### Source code on Github

All the Python code is available on [Github](https://github.com/phoenix-journey/iss)

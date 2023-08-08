---
title: "Bing Search"
description: "Search queries in terminal using Bing search engine."
lead: "Search queries in terminal using Bing search engine."
date: 2023-01-28T07:17:31+01:00
lastmod: 2023-01-28T07:17:31+01:00
draft: false
images: []
menu:
  docs:
    parent: "tools"
    identifier: "bing-search-9d5e78a979cbbdb53bcd17fe6c632f8a"
weight: 999
toc: true
---

 and explore 🌍

<img src="https://img.shields.io/crates/v/bing-search.svg" alt="Crates.io">

Using `bing-search` you can find information that you want. Although
limited to displaying only headers, just like on the graphical interface
during initial look up, it might help you tackle your problems better.

Combined with `w3m` - _terminal web browser_ you can practically not miss
the needle in a haystack, and equiped with proper knowledge of search
queries syntax, you can achieve magic ✨!

## Basics

Simple usage can't be simpler:

```shell
bing-search "Where is Poland?"
```

## Combine with w3m

then you can copy the address of the website and use it with `w3m`

```shell
w3m https://some.text.only.website
```

## Refine your search to look for .txt files

To refine your search and look for only `.txt` files in your search
you can use this syntax:

```shell
bing-search "how to cook pancakes filetype:txt"
```

## More results

Te get more results printed from your search type this:

```shell
bing-search "katy perry" 100
```

## Exclude words

If you would like to search for Katy Perry but without Orlando Bloom you
will type... something with `-`

```shell
bing-search "Katy Perry -Orlando-Bloom"
```

## Only on one site

To look for searches only on one site you would write it like that

```shell
bing-search "site:rollingstone.com Katy Perry"
```

## To look for answers in one language...

...You would type

```shell
bing-search "language:ro Katy Perry"
```

## If you want specific dates

Then you want to include this in your search

```shell
bing-search "y2k date:1999-01-01..2001-12-31"
```

## Location

Search for a specific location: Use `location:` operator to search for pages related to a specific location, for example:

```shell
bing-search "pancakes recipe location:Paris"
```

## Word in title of webpage

To search for specific words in the title, use `intitle:` operator to search for pages that have a specific word in the title, for example:

```shell
bing-search "intitle:pancakes recipe"
```

## In URL

Search for specific words in the URL, use `inurl:` operator to search for pages that have a specific word in the URL, for example:

```shell
bing-search "inurl:pancakes recipe"
```

## Search for a specific link

Use `link:` operator to search for pages that link to a specific URL, for example:

```shell
bing-search "link:https://example.com/pancakes-recipe"
```

## Search for synonyms

Use `~` operator to search for pages that contain synonyms of a specific word, for example:

```shell
bing-search "~pancakes recipe"
```

## Search for a specific phrase:

Use `"` operator to search for pages that contain a specific phrase, for example:

```shell
bing-search "\"Katy Perry Part of Me lyrics\""
```

Here, you have to escape the inner `"` with `\` backslash like that `\" somthing \"`

## Search for a specific word

Use `+` operator to search for pages that contain a specific word, for example:

```shell
bing-search "+pancakes +recipe"
```

## Search for images

Use `--image` switch to search for images, for example:

```shell
bing-search --image "pancakes recipe"
```

Currently supported on Linux and macOS. Also works in Nutek Terminal container.

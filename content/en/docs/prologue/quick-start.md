---
title: "Quick Start for Nutek Security Platform"
description: "Nutek is a set of tools that you can install automatically using Homebrew to save resources and gain an edge against your target."
lead: "Nutek is a set of tools that you can install automatically using Homebrew to save resources and gain an edge against your target"
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
images: []
menu:
  docs:
    parent: "prologue"
weight: 110
toc: true
---

## Requirements

* [Homebrew 🍺](https://brew.sh) - package manager for macOS

{{< details "Download size?" >}}
Download size might be significant. Please be aware that on metered connections it might use the full bandwith and incure some additional costs.
{{< /details >}}

## Get your nutek-apple.rb copy

You're really close to having the best there is in a fraction of a cent (don't forget to support the developers!)

Get your copy of `nutek-apple.rb`, in a way that suits you the most.

You can:

* copy the content and paste it in your text editor
* download just this file
* zip and download the repository
* clone the whole project (you will get updates on `git pull origin main` command)

{{< alert icon="👉" text="Cloning easily enables you to update `nutek-apple.rb` when the new version will come out." />}}

## Chose your set of packages

First run.

```shell
ruby nutek-apple.rb`
```

This will show the help message. From there you might already know what
you want, but the most common option is to use

```shell
ruby nutek-apple.rb -i --all --unattended
```

After running this command, you won't be prompted for confirmation and
all the default packages will be installed without any exception.

Or if you wish to only get _knowledge_ (by what I mean reconnaisance) kind of apps

```shell
ruby nutek-apple.rb --install --knowledge
```

This will show you the packages that will be installed and prompt you to
chose if that's ok and then install all of them.

## That's it

There is nothing more to do next, maybe beside:

```shell
ruby nutek-apple.rb --safari
```

Which will bring up this website with tools panel opened to the left
where you can find all of the apps that are included with brief
explenation.

{{< details "Can't see?" >}}
Simply click the TOOLS to the left, and the apps will roll...
{{< /details >}}

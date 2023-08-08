---
title: "Hugo. My First Website"
description: "Creating website using static site generatior Hugo."
lead: "Creating website using static site generatior Hugo."
date: 2022-12-30T17:57:31Z
lastmod: 2022-12-30T17:57:31Z
draft: false
menu:
  docs:
    parent: "tools"
weight: 150
toc: true
---

## Create **YOUR** first website

Hej!

This New Year's Eve you have so many new resolutions that you need
to get them into one place, and make them public, so you can be
as transparent as your nearest politician is.

So you heard that there is GitHub, Nutek, Szymon, Hugo and whoever
I have to mention to make you test this, because it's so awesome to
have your own *static* website build with [Hugo](https://gohugo.io/) *Markdown* and all crazy stuff.

### You should already have:

- an account on **GitHub** and *git* of course;
- `Docker`, because you're a good person and want to stick with what
Nutek has to offer;
- 30 minutes before midnight;
- Visual Studio Code, or you're already a masters degree in (N)Vim

### Basic scaffolding

```shell
 your Nutek and type this into terminal to install Hugo
apt update && apt install hugo
 for any reason you don't use Nutek yet but you have Docker,
 Docker and then in your 'other' terminal run this to install
 - static website generator:
docker pull klakegg/hugo

 you're on Windows (Powershell) copy and paste #1 otherwise #2,
 you also may run it outside docker, then #3
#1, or
docker run --rm -it -v ${PWD}:/src klakegg/hugo new site my-website
#2, or
docker run --rm -it -v $(pwd):/src klakegg/hugo new site my-website
#3 - if you already installed Hugo using any other way
hugo new site my-website
 you have a website, let's get into it's folder
cd my-website
 git repository
git init
 simple theme to start with
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke themes/ananke
echo "theme = 'ananke'" >> config.toml
```

### Now we're making resolutions, right?

#### Create post

Create your first post on this brand new website with super-simple
terminal command:

`hugo new posts/my-2023-resolutions.md`

or if you're following with *Docker* Hugo build:

`docker run --rm -it -v ${PWD}:/src klakegg/hugo new posts/my-2023-resolutions.md` - Windows

`docker run --rm -it -v $(pwd):/src klakegg/hugo new posts/my-2023-resolutions.md` - Linux and MacOS

If everything goes well on the machine side, you should have a blank
page, where you could tell everyone who's caring enough about you (or
simply curious enough), what your resolutions are... Maybe you have
just one, like not giving up on you hobbies, or remember about buying
those yoga pants, because pandemic is long gone, but your shape is not
in the right tuning... Whatever the details, put them here using *[Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)* syntax. I will give you the basics.

#### Markdown basics

Open file `my-2023-resolutions.md` in `content/posts` folder. Leave the top of the file as it is (change *draft* to **false** when you're done) and start with a second-order header like so:

`## My 2023 Resolutions`

## My 2023 Resolutions

After that you can place a horizontal rule:

`___`

___

Start with you goals list:

```markdown
1. Be a nice person
    - because humans are friendly
    - karma goes both ways
2. Learn just to learn
    * I don't need a collage degree to play a guitar
3. Redesign my desk, because I look for peace (little bonzai might help)
![Example image](/static/img/image.png)
```

1. Be a nice person
    - because humans are friendly
    - karma goes both ways
2. Learn just to learn
    - I don't need a collage degree to play guitar
3. Redesign my desk, because I look for peace (little bonzai might help)
![Example image](https://web.archive.org/web/20010629034653im_/http://republika.pl/szymonbla/squirtle.gif)

Then fantasize a little bit with paragraphs, emphasis and a link:

```markdown
Write an [email](mailto:santa@kremlin.ru) to **Santa**, where I ask to
have the best experience human can get - *love*

Then maybe divorce on 14th February...
```

Write an [email](mailto:santa@kremlin.ru) to **Santa**, where I ask to
have the best experience human can get - *love*

Then maybe divorce on 14th February...

Buld a table with your party budget:

```markdown
| Day | Club | DJing |
| --- | --- | --- |
| Friday | London | $1600 |
| Saturday | Paris | $12 |
| Sunday | Berlin | $1 |
```

| Day | Club | DJing |
| --- | --- | --- |
| Friday | London | $1600 |
| Saturday | Paris | $12 |
| Sunday | Berlin | $1 |

And voilà!

### Local development server

Spin-up your local server with drafts rendered:

```shell
 on Windows
docker run --rm -it -v ${PWD}:/src klakegg/hugo server --buildDrafts
```

```shell
 on Linux and MacOS
docker run --rm -it -v $(pwd):/src klakegg/hugo server --buildDrafts
```

```shell
 Hugo
hugo server --buildDrafts
```

### Satisfied?

#### End draft phase

Edit your resolution markdown file and on top of if change `draf: true`
to `draft: false`

#### Immidietly make production version

```shell
 on Windows
docker run --rm -it -v ${PWD}:/src klakegg/hugo
 on Linux, MacOS
docker run --rm -it -v $(pwd):/src klakegg/hugo
 Hugo
hugo
```

#### Create repository on GitHub

Go to [GitHub](https://github.com), login, or sign up if you don't
have an account already - it's free, and it's home to many of other free or open source projects. Don't be afraid, it's just good idea
to have such an account, but you can deploy your website to many other places. [Here](https://gohugo.io/hosting-and-deployment/) is how to do so.

If you're following this guide, as you should be ;) look on the GitHub's
site about creating a [GitHub Page](https://pages.github.com/) using
other tools like **[Jekyll](https://jekyllrb.com/)**. In case you're
unsure what *you* should use, try to Google this phrase 'jekyll vs hugo'

...Thank you, for following my guide, now please create a repository
according to [GitHub Page](https://pages.github.com/) address you want
to have. If you're opting-in for custom domain, I will show you to get
this done too. Nevertheless you need any GitHub address to start with.

1. create new repository `The GitHub Page Way`
2. add remote to your local git repository with
`git remote add origin xxx.git` (replace xxx with your repository
address).
3. when you're done with your resolutions post, commit all your
work:

```shell
git status
git add *
git status
 there are some files left, manually add them with:
git add path/to/file1 path/to/file2 path/to/file3
 flip the slashes for Windows
git add path\to\file1 path\to\file2 path\to\file3
```

Commit with this command that does the foundation commit (think of it
as a update to your portfolio, new verse in your song, or a new chapter
in a book) itself along with a required message:

`git commit -m "Add my 2023 resolutions"`

#### Double check draf: false

Change draft to false on top of resolutions post file.

### Configuration

#### config.toml

Open `config.toml` file in root of the project.

Set:

- `baseURL = 'http://user.github.io/'` or
- `baseURL = 'http://user.github.io/repository/'` or
- `baseURL = 'http://example.com/'`

Then set:

`languageCode = 'en-us'`

and

`title = 'John Dillinger'`

and

`theme = 'ananke'`

### Deploy to GitHub Pages

#### Workflow file

Create `.github/workflows/gh-pages.yml` file with this specific content:

```yaml
name: github pages

on:
  push:
    branches:
      - main  # Set a branch that will trigger a deployment
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v3
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref == 'refs/heads/main'
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

This file, when you push your code to GitHub will run the necessairly
steps to create the machine readeble representation of what you've
created and it will create gh-pages branch from which you will
serve your website.

Check status of this workflow in Actions tab of your repository.
This is super-important. Without this action/workflow finishing properly
you can't the desired result.

BTW GitHub actions are capable of many more and cmplex things. They
can build your whole application and prepare it to run on clients
machines without you needeing to build all the binaries on your
hardware.

[Check this out](https://github.com/features/actions)

#### Excerpt from Hugo website

##### GitHub pages setting

By default, the GitHub action pushes the generated content to the
gh-pages branch. This means GitHub has to serve your `gh-pages`
branch as a GitHub Pages branch. You can change this setting by
going to `Settings` > `Pages`, and change the source branch to
`gh-pages`.

### Use a Custom Domain

#### Create CNAME file (another excerpt from Hugo website)

If you’d like to use a custom domain for your GitHub Pages site, create
a file `static/CNAME`. Your custom domain name should be the only
contents inside `CNAME`. Since it’s inside static, the published site
will contain the `CNAME` file at the root of the published site, which
is a *requirement* of GitHub Pages.

Refer to the [official documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site) for custom domains for further information.

#### Subdomain

Go to your domain's DNS provider, and add `CNAME` record for page.your.doman pointing to your GitHub Pages address, for example
`phoenix-journey.github.io.`. The actual process vary from provider, to
provider. In the core it's just it.

#### Example.com

If you want to host your GitHub Page using your domain.com address, then create

`A` record with this ip addresses:

- 185.199.108.153
- 185.199.109.153
- 185.199.110.153
- 185.199.111.153

Maybe then `AAAA` record with this ip addresses:

- 2606:50c0:8000::153
- 2606:50c0:8001::153
- 2606:50c0:8002::153
- 2606:50c0:8003::153

#### WWW

You might want to create `CNAME` with `www.your-domain.com`

#### Final touch

1. Open your GitHub Page repository `Settings`, got to `Pages` and set your `Custom domain`. If everything goes well and DNS records spreading around the world...
2. You might even get an option to **make it HTTPS**! Just *Enforce HTTPS* checkbox and you're good to go o7

### Inspiration

For inspiration, take a look at Phoenix Journey's repository for
[this website](https://github.com/nutek-terminal/nutek-terminal.github.io) written using the same tools, that's been thaught here.

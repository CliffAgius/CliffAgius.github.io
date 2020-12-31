---
draft:      true
layout:     post
title:       "Setup Hugo With Github Pages"
subtitle:    ""
description: "Moving from Ghost blog host on Azure to Hugo on Github Pages..."
date:        2020-10-16
image:       "images/.png"
tags:        ["Xamarin"]
categories:  ["" ]
---

# What and Why?

So I have hosted my blog using Ghost on Azure Websites for over a year now and in that time I have found it hard to write blogs as much as I would like.  The reason being that I tend to have a lot of time either in the air or downroute somewhere with no data connection, plus I found the Ghost offering for writing Offline not that easy.

Yes I could write the post but then needed to tweak and play with uploading it using the Admin page of Ghost that took a good 10-15 minutes each time.  Now I confess I may have been doing it wrong but the other reason for the move is the fact that GitHub Pages is well FREE!!! Yes totally free.

## Where did I start?

I started as we all do Bingoogling and looking around, the [Hugo Docs](https://gohugo.io/) are very good and explain how to set-up Hugo locally but not how to host on Github (Not at the time of writing anyway!) plus I didn't feel there was an End-to-End process of how to do this, but fear not here is one (I Hope!)

## Installing Hugo

First we need to install Hugo locally and set-up ready for your awesome blogging website. Now I am a Windows user and I have the awesome [Chocolatey](https://chocolatey.org/) installed so I just used:

    choco install hugo -confirm

If you don't have Chocolatey installed you can just use:

    Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

But as I know you may not be using the same setup as me head to the [Hugo Docs](https://gohugo.io/getting-started/installing) and find your set-up.

Now we have it installed let just be sure it works, so from your favorite command line enter:

    hugo version

You should see womething like this:

![](2020-12-03-19-44-52.png)

## Create your Blog Site

Now that we have the Hugo tooling installed we need to create our site and this couldn't be any simpler you just need to run:

    hugo new site MyFancyBlog

This will create a new Blog site in a folder named `MyFancyBlog` so choose wisely!

Now if we `cd` into that folder we should see something like this:

![BlogSiteFolderContents](2020-12-03-21-28-41.png)

And that is your new blog site as simple as that...

## Adding a Theme

Now that we have a site we need to add a theme so that it looks pretty, amd this is the first point I diverge from the Hugo Docs.  In the docs it suggest that you add a Theme as a `git` submodule, which is find as long as that theme is exactly what you want.  However if you want to use a theme as a starting point and edit from there you may want to do what I did and fork the Theme into your project.

So go pick a theme from [https://themes.gohugo.io/](https://themes.gohugo.io/) there are 1000's so take your time I'll wait here for you...

Right so you picked the theme lets add it, so go into the folder you created earlier and we need to make it a `git` repository so that we can track the changes and push to GitHub later.

    git init
    cd themes
    git clone https://github.com/budparr/gohugo-theme-ananke.git

This will clone the `anake` theme into the themes folder so that you can edit and change the theme as you see fit.  

However we need to tel Hugo to use this theme when it does it's builds, so using your favorite text editor which should be [VSCode](https://code.visualstudio.com/) in which case from the command line you can use:

    code .

which will open the folder in VSCode ready to edit. So now open the `config.toml` file and add:

    theme = "gohugo-theme-ananke"

While your in here you can set the Base-URL to your new blog sites URL and obviously change the title etc.  It's pretty obvious what you need to change as there are only 3 lines.

##  Test

Now we have a theme and all the bits set we can test to see what we have, and this is where Hugo is great as you can run the server locally to see exactly what it will look like when it's live.  You don't need anything other than:

    hugo server -D

This is build the files and host them on LocalHost for you, in your terminal you shoudl see something like:

![RunningHugoServer](2020-12-03-21-54-01.png)
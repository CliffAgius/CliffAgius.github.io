---
draft:      false
layout:     post
title:       "Ideas For a Visual Studio Tool"
subtitle:    ""
description: "An Idea of mine for making Images easier to work with in Visual Studio when building a new Xamarin App that targets Andriod/iOS and UWP..."
date:        2020-03-03
image:       "images/MobileSim.jpg"
tags:        ["Xamarin"]
categories:  ["Xamarin" ]
---

# Idea for a VisualStudio Tool for Xamarin

In my last blog I wrote about all the different image sizes required for a Xamarin project and how to calculate them and size them and where to put them, it's all very confusing when you first start out in mobile development so I hope that post helped...

Recently (2019!) I was working on a standalone UWP project for a new instructor control station in the Mobile Flight Sim I helped to build, this sim is used by the airline I work for at School STEM events, Recruitment and fun corporate events. It travels to events all over the UK and EU (Have to write that now 😥) and this new Instructor station allows the pilots at the event to control the sim.

![Mobile Sim](/images/MobileSim.jpg)

While working on this project I needed to add some image resources for the Application Icons and Splash screen etc and writing the last post this is where my idea come from.

In a Xamarin project we need to resize an image many times and place them into the correct folders then include them in the project before repeating the process for the next image... this is all very tedious and time consuming BUT... What if there was a tool that could do this for you...

## VisualStudio to the rescue

Well I say to the rescue it will need the Microsoft teams to do some work but I am hoping that this blog post will explain my idea and if enough of you reading this can pester them they may work on it.

So if you go File New -> UWP project and when it's finished creating the project you find and open the Package.appxmanifest which should be the last item in the Solution Explorer.

![Package.appxmanifest](/images/PackageManifestFile.jpg)


When you open this you will see a Visual Assets Tab, click this.


![Visual Assets Tab](/images/VisualAssetsTab.jpg)

![Asset Generator](/images/AssetGenerator.jpg)

This is the magic tool you use in a UWP project to automatically create your project assets, the likes of your Tiles, App Icons etc.  Essentially what this tool does is you drop an image into the Source window or select using the Source ellipsis from your file system.  Click the Generate button and it works away for a short time and crops/sizes and saves the image in the correct sizes in the correct place in the project.

## Now how can this help in Xamarin?

Well we have two ways of using an image, sticking an image into the shared project and using the ImageResourceExtension class to find and use the file or we place multiple copies of the image into the various Android and IOS folders all correctly sized and named.

What if the clever people at Microsoft and Xamarin take this already existing tool inside Visual Studio and repurposed it...  What if we place our images in the Shared Project and then use this tool to automatically resize them and place them into the xhdpi folder and create the IOS AssetCatalog.

The tool already generates the files for UWP so that work is done all is needed is a few extra lines in the Tool to show the output for the Android and IOS version of the image.

They could also add a size picker near the top so that you can select the sizes you want the Base version to be remembering the little DPI table from my last post

![DPI_Chart](/images/DPI_Chart.jpg)

With this info the tool can automatically create the others based off this and place them correctly in the project, even use the current Image Size tool which is reformatted to show a Mobile Phone screen and the size the image would look when converted so it's easy to pick the one you want a bit like this (Button Mobile Phone Outline in place of the Box!)

![Generated Images](/images/GeneratedImages.jpg)

Once you have reviewed and tinkered with say being able to drag the master image around to show where the crop/cuts would be made for the size you have picked click another button to place the images into the respective folders in the project.

## Do you like?

I think this idea will work and save a lot of time editing photo's as well as making the onboarding of new dev's to the Xamarin platform easier.  VisualStudio is an amazing IDE and has the power to edit the images even if just a basic first pass while you await the designers to send you the final edits.  

MFractor is also an amazing tool that brings a lot more than just image editing to the VS4Mac and VS19 but it come at a price which in my mind isn't expensive if I'm honest but to a new dev starting out trying to work out if Xamarin is for them any cost is too much and barriers like a simple image edit too high.

If you think this idea would be good then copy the link of this blog and pester the Xamarin and Microsoft teams and lets see if they will edit the tool for our needs, yes I could write an Add-On but this already exists now for UWP and just needs a tweak and it will be in the box for everyone. (Sorry MFractor)

Well that's my idea.

Happy coding

Cliff.


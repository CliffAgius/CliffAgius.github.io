---
draft:      false
layout:     post
title:       "Xamarin.Forms NEW Expander Control"
subtitle:    ""
description: "Coming along in the new Xamarin.Forms 4.6 release which at the time of writing is at 4.6pre4 (So it's due very soon!) is a new control called the ExpanderControl"
date:        2020-04-23
image:       "images/Nuget.jpg"
tags:        ["Xamarin"]
categories:  ["Xamarin" ]
---

# Xamarin.Forms NEW ExpanderControl

Coming along in the new Xamarin.Forms 4.6 release which at the time of writing is at 4.6pre4 (So it's due very soon!) is a new control called the ExpanderControl, now those of you that have played with Web will know this as the Accordian Control in that the user clicks/taps the element in the list and it expands to show more detail of that item.

This control has been added to Xamarin.Forms by Community member [Andrei Misiukevich](https://github.com/AndreiMisiukevich) thanks for the great work Andrei.

## Where to Start.

First you need to make sure that you have at least Xamarin.Forms 4.6 or greater so head over to Manage Nuget Packages and select the Updates tab at the top, and you will see a list of available updates (I'm doing this before 4.6 is released so I need to select the pre-release so show the coming toys...)

![Nuget](/images/Nuget.jpg)

## How to Add the Control.

Sadly at the time of writing (Apr2020) there are no Docs for this control other than what the creator produced in the [GitHub PR](https://github.com/xamarin/Xamarin.Forms/pull/9044) for this control but I am sure there will be some Docs along soon.

The important part and the bit that is easy to miss is that this control is still Experimental so you need to add the flag to your projects otherwise it won't work and you'll be wondering why.

In your Android `MainActivity.cs` add the SetFlags line above the `Forms.Init` here I also have the CollectionView to show how you add more than one Flag, it's just a String Array.


     Xamarin.Forms.Forms.SetFlags(new string[] {"CollectionView_Experimental", "Expander_Experimental"});

For iOS it's in your `AppDelegate.cs` in the same place before the `Forms.Init` line.

     global::Xamarin.Forms.Forms.SetFlags(new string[] { "CollectionView_Experimental", "Expander_Experimental"});


## How to use the control

So in your XAML (yes you can do C# as well but I prefer XAML for UI) you need to add the following:

    <Expander>
        <Expander.Header>
            <Label Text="Header" />                     <-- What your user will see Un-Expanded
        <Expander.Header>
        <Expander.ContentTemplate>
            <DataTemplate>
                <StackLayout>
                    <Label Text="Content Line 1" />     <-- Content users will see when they expand.
                    <Label Text="Content Line 2" />
                <StackLayout>
            <DataTemplate>
        <Expander.ContentTemplate>
    <Expander>

So what is happening here is that inside the Expander control you have a Header and Content section and as the name suggests you have the Header which is the content the User will see when the Control is closed or un-expanded and the Content section is what extra content will be displayed when the Control is tapped/clicked and it opens.

There are also values you can change for settings like the Animation length when opening and closing and the Easing how quickly it starts the animation:

    public uint ExpandAnimationLength { get; set; }

    public uint CollapseAnimationLength { get; set; }

    public Easing ExpandAnimationEasing { get; set; }

    public Easing CollapseAnimationEasing { get; set; }

## What does it look like.

With a few lines of code added to the `File->New` of a Xamarin Shell page like this:

    <?xml version="1.0" encoding="utf-8" ?>
    <ContentPage
        x:Class="ExpanderControl.Views.ItemsPage"
        xmlns="http://xamarin.com/schemas/2014/forms"
        xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
        xmlns:d="http://xamarin.com/schemas/2014/forms/design"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        x:Name="BrowseItemsPage"
        Title="{Binding Title}"
        mc:Ignorable="d">
    
        <ContentPage.ToolbarItems>
            <ToolbarItem Clicked="AddItem_Clicked" Text="Add" />
        </ContentPage.ToolbarItems>
    
        <RefreshView Command="{Binding LoadItemsCommand}" IsRefreshing="{Binding IsBusy, Mode=TwoWay}">
            <CollectionView x:Name="ItemsCollectionView" ItemsSource="{Binding Items}">
                <CollectionView.ItemTemplate>
                    <DataTemplate>
                        <Expander>
                            <Expander.Header>
                                <Label
                                    Padding="5"
                                    BackgroundColor="BurlyWood"
                                    FontSize="16"
                                    LineBreakMode="NoWrap"
                                    Style="{DynamicResource ListItemTextStyle}"
                                    Text="{Binding Text}" />
                            </Expander.Header>
                            <Expander.Content>
                                <Label
                                    Padding="5"
                                    BackgroundColor="LightBlue"
                                    FontSize="13"
                                    LineBreakMode="WordWrap"
                                    Style="{DynamicResource ListItemDetailTextStyle}"
                                    Text="{Binding Description}" />
                            </Expander.Content>
                        </Expander>
                    </DataTemplate>
                </CollectionView.ItemTemplate>
            </CollectionView>
        </RefreshView>
    </ContentPage>

You get a nice simple control on the page like this: (I Like planes OK...)

![WizzyStuff](/images/DroidSample.gif)

## Conclusion

This is a simple control and one that means you can cram more information onto the screen by allowing the user to expand an item rather than tap to goto a details page.

It's been missing from Xamarin.Forms for a while if you ask me but thanks to the Hard work of Andrei Misiukevich a community member Like you and me it has been added to the Xamarin toolset for us all to enjoy.

I'm already using it in a live project and so far the testing hasn't shown any issues so that Experimental flag may not be around forever, however if you want to see what flags are active for the current Stable release then check out [docs.microsoft.com](https://docs.microsoft.com/xamarin/xamarin-forms/internals/experimental-flags?WT.mc_id=DOP-MVP-5003764)

I hope this helped and feel free to reach out in the usual places or leave a message below.

Oh! And if your wondering why I picked Brown for the colour of the Header elements... Well anyone that's seen a Boeing Flightdeck (Other than the 787) knows of the Boeing ermmm Brown... ;-)

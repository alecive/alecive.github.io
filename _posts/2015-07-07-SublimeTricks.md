---
layout: post
title: Sublime Tricks
link: https://github.com/alecive/periPersonalSpace
link-alt: Sublime Website
date: 2015-07-07
category: blog
description: Tricks, packages and more stuff that I use on Sublime Text Editor
article: yes

---

# Contents
{:.no_toc}

* This line will be replaced by the ToC, excluding the "Contents" header
{:toc}

# Color Picker

GitHub repo → [https://github.com/weslly/ColorPicker](https://github.com/weslly/ColorPicker)

Gives you the ability to change colors with a color picker on the fly. To insert or change a selected color, use: `ctrl+shift+c`

By default, the hex color code is inserted using uppercase letters (`#ABCDEF`, for example). To use lowercase letters (`#abcdef`) instead, copy the contents of `Preferences → Package Settings → ColorPicker → Settings—Default` to the empty file created by selecting `Preferences → Package Settings → ColorPicker → Settings—User`, then change "color_upper_case" to false.

# Doc Blockr

A really great way to easily create doc blocks for many languages including JavaScript, PHP, and CoffeeScript. Just type in `/**` above your function and press `tab`. Watch the magic as DocBlockr takes the function name and variables and creates your doc block.

# GitGutter

This is a small, but useful plugin that will tell you what lines have changed since your last Git commit. An indicator will show in the gutter next to the line numbers.

# Git

After installing the Git package, if you open your command palette by using `ctrl + shift + p`, then you’ll see your available Git commands (a ton!).

The cool thing is that like all other times you use the command palette, you don't have to enter the entire command. Sublime Text will autocomplete things for you. So instead of typing `git add -A`, you can just type `add` and Sublime Text will know! Just another way to shave off milliseconds off your workflow.

## Commit vs Quick Commit

There are two commit commands the Sublime Text Git Plugin provides. The main difference is that _Quick Commit_ will open up a little text box that you can quickly type into while _Commit_ will open a new file and show you the changes in each file.

## Add, Commit, and Push Within Sublime Text

My workflow when trying to push code to the server inside of Sublime Text looks like:

 * <kbd>ctrl + shift + p</kbd>
 * TYPE <kbd>add</kbd>
 * <kbd>ctrl + shift + p</kbd>
 * TYPE <kbd>quick</kbd> THEN <kbd>type message</kbd>
 * <kbd>ctrl + shift + p</kbd>
 * TYPE <kbd>push</kbd>


## Staging Files and Committing In One Step

To add and commit all in one step, just skip straight to the Quick Commit command. That will stage and commit for you. It’s the equivalent of `git commit -am 'im staging and committing!'`. 

# Theme: SpaceGray

Available here: [https://github.com/kkga/spacegray](https://github.com/kkga/spacegray)

A set of custom UI themes for Sublime Text 2/3. It's all about hype and minimal. Comes in different flavors with accompanying [Base16](https://github.com/chriskempson/base16) color schemes.

It's the best one, available in three options:

## How to Activate

Activate the UI theme and color scheme by modifying your user preferences file, which you can find using the menu item `Sublime Text -> Preferences -> Settings - User` (<kbd>⌘</kbd><kbd>,</kbd> on Mac).

You can choose whichever flavor you like, but don't forget to change *both* color scheme and UI theme so they match.

***Note: Don't forget to restart Sublime Text after activating the theme.***

### Spacegray

Default flavor based on Base16 Ocean Dark color scheme.

{% highlight json linenos %}
{
  "theme": "Spacegray.sublime-theme",
  "color_scheme": "Packages/Theme - Spacegray/base16-ocean.dark.tmTheme"
}
{% endhighlight %}

### Spacegray Light

Light variation based on Base16 Ocean Light color scheme.

{% highlight json linenos %}
{
  "theme": "Spacegray Light.sublime-theme",
  "color_scheme": "Packages/Theme - Spacegray/base16-ocean.light.tmTheme"
}
{% endhighlight %}

### Spacegray Eighties

A variation based on Base16 Eighties Dark color scheme.

{% highlight json linenos %}
{
  "theme": "Spacegray Eighties.sublime-theme",
  "color_scheme": "Packages/Theme - Spacegray/base16-eighties.dark.tmTheme"
}
{% endhighlight %}

### Misc options I'm using

{% highlight json linenos %}
{
  "spacegray_sidebar_font_small": true,
  "spacegray_tabs_font_normal"  : true,
  "spacegray_tabs_xlarge"       : true,
  "spacegray_tabs_auto_width"   : true,
}
{% endhighlight %}
 

---
title: Sublime Tricks
link:
link-alt:
date: 2015-07-07
category: blog
description: Tips and tricks for Sublime Text Editor
tags: [blog,how to,tutorial,sublime text,tips and tricks]
type: article
permalink: sublime_tricks.html

---

# Contents
{:.no_toc}

* This line will be replaced by the ToC, excluding the "Contents" header
{:toc}

# Color Picker

GitHub repo: [https://github.com/weslly/ColorPicker](https://github.com/weslly/ColorPicker)

Gives you the ability to change colors with a color picker on the fly. To insert or change a selected color, use `ctrl+shift+c`.
By default, the hex color code is inserted using uppercase letters (`#ABCDEF`, for example). To use lowercase letters (`#abcdef`) instead, copy the contents of `Preferences` → `Package Settings` → `ColorPicker` → `Settings—Default` to the empty file created by selecting `Preferences` → `Package Settings` → `ColorPicker` → `Settings—User`, then change `color_upper_case` to false.

# Terminal

Package link: [https://packagecontrol.io/packages/Terminal](https://packagecontrol.io/packages/Terminal)

Adds shortcuts and menu entries for opening a terminal at the current file, or the current root project folder in Sublime Text. I really love this feature!

## Features

 * To open a terminal in the folder containing the currently edited file, press `ctrl+shift+t` on Windows and Linux, or `cmd+shift+t` on OS X
 * To open a terminal in the project folder containing the currently edited file, press `ctrl+alt+shift+t` on Windows and Linux, or `cmd+alt+shift+t` on OS X

In addition to the key bindings, terminals can also be opened via the editor context menu and the sidebar context menus.

The only problem is that the `ctrl+shift+t` key binding is already associated with the "Reopen closed file" feature that I use a lot. In order to avoid overlapping, I decided to move these key bindings to `ctrl+alt+t` and `ctrl+alt+shift+t`. Custom key bindings such as this would be added to the file opened when accessing the `Preferences` → `Key Bindings – User` menu entry (the file name varies by operating system).

~~~json
[
  { "keys": ["ctrl+shift+7"],      "command": "toggle_comment",   "args": { "block": false } },
  { "keys": ["alt+m"],             "command": "markdown_preview", "args": {"target": "browser", "parser":"markdown"} },
  { "keys": ["ctrl+alt+t"],        "command": "open_terminal" },
  { "keys": ["ctrl+alt+shift+t"],  "command": "open_terminal_project_folder" }
]
~~~

# Enable auto quotes for grave accents

For standard single and double quotes, sublime text allows you to select text and hit a quote key to wrap the selected text in the quote. For example, `hello world` becomes `"hello world"`.
However, there is no default way to perform the same action with grave accents (`).
I found the solution [here](http://stackoverflow.com/a/16346444/3333040): the auto pairing is simply a few specialized key bindings. These custom key bindings (see above on how to set them) should do the trick:

~~~json
[
{ "keys": ["`"], "command": "insert_snippet", "args": {"contents": "`$0`"}, "context":
  [
    { "key": "setting.auto_match_enabled", "operator": "equal", "operand": true },
    { "key": "selection_empty", "operator": "equal", "operand": true, "match_all": true },
    { "key": "following_text", "operator": "regex_contains", "operand": "^(?:\t| |\\)|]|;|\\}|$)", "match_all": true }
  ]
},
{ "keys": ["`"], "command": "insert_snippet", "args": {"contents": "`${0:$SELECTION}`"}, "context":
  [
    { "key": "setting.auto_match_enabled", "operator": "equal", "operand": true },
    { "key": "selection_empty", "operator": "equal", "operand": false, "match_all": true }
  ]
},
{ "keys": ["`"], "command": "move", "args": {"by": "characters", "forward": true}, "context":
  [
    { "key": "setting.auto_match_enabled", "operator": "equal", "operand": true },
    { "key": "selection_empty", "operator": "equal", "operand": true, "match_all": true },
    { "key": "following_text", "operator": "regex_contains", "operand": "^`", "match_all": true }
  ]
},
{ "keys": ["backspace"], "command": "run_macro_file", "args": {"file": "Packages/Default/Delete Left Right.sublime-macro"}, "context":
  [
    { "key": "setting.auto_match_enabled", "operator": "equal", "operand": true },
    { "key": "selection_empty", "operator": "equal", "operand": true, "match_all": true },
    { "key": "preceding_text", "operator": "regex_contains", "operand": "`$", "match_all": true },
    { "key": "following_text", "operator": "regex_contains", "operand": "^`", "match_all": true }
  ]
}
]
~~~

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

 * `ctrl + shift + p`
 * TYPE `add`
 * `ctrl + shift + p`
 * TYPE `quick` THEN `type message`
 * `ctrl + shift + p`
 * TYPE `push`


## Staging Files and Committing In One Step

To add and commit all in one step, just skip straight to the Quick Commit command. That will stage and commit for you. It’s the equivalent of `git commit -am 'I'm staging and committing!'`.

# Theme: SpaceGray

Available here: [https://github.com/kkga/spacegray](https://github.com/kkga/spacegray)

A set of custom UI themes for Sublime Text 2/3. It's all about hype and minimal. Comes in different flavors with accompanying [Base16](https://github.com/chriskempson/base16) color schemes.

It's the best one, available in three options:

## How to Activate

Activate the UI theme and color scheme by modifying your user preferences file, which you can find using the menu item `Sublime Text -> Preferences -> Settings - User` (`⌘` `,` on Mac).

You can choose whichever flavor you like, but don't forget to change *both* color scheme and UI theme so they match.

***Note: Don't forget to restart Sublime Text after activating the theme.***

### Spacegray

Default flavor based on Base16 Ocean Dark color scheme.

~~~json
{
  "theme": "Spacegray.sublime-theme",
  "color_scheme": "Packages/Theme - Spacegray/base16-ocean.dark.tmTheme"
}
~~~

### Spacegray Light

Light variation based on Base16 Ocean Light color scheme.

~~~json
{
  "theme": "Spacegray Light.sublime-theme",
  "color_scheme": "Packages/Theme - Spacegray/base16-ocean.light.tmTheme"
}
~~~

### Spacegray Eighties

A variation based on Base16 Eighties Dark color scheme.

~~~json
{
  "theme": "Spacegray Eighties.sublime-theme",
  "color_scheme": "Packages/Theme - Spacegray/base16-eighties.dark.tmTheme"
}
~~~

### Misc options I'm using

~~~json
{
  "spacegray_sidebar_font_small": true,
  "spacegray_tabs_font_normal"  : true,
  "spacegray_tabs_xlarge"       : true,
  "spacegray_tabs_auto_width"   : true
}
~~~


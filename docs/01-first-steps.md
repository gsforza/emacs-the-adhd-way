# First startup
Just for reference, I am using Emacs 26.3 on Fedora 31 Workstation.

When first launching Emacs, you will be presented with this:  


Here one can start the `Emacs Tutorial`, view the `manual` or do various other things. All the links are clickable. But of course, we are not learning Emacs to just click on things, are we?

To learn the basics of moving around in Emacs and also get some basic info about the multitude of aspects of Emacs, I will start by going through the tutorial. Whenever I started using Emacs, I always neglected the tutorial and dived head-first into using Emacs, not even learning the basics of moving around, because I always installed `evil` as soon as possible.

This time, I will force myself through the whole tutorial and also, although stated differently earlier, I will not install `evil` from the get-go and stay with the built-in keybindings.

# Emacs Tutorial
## Basic movement
- Move one screen down: `C-v`  
- Move one screen up: `M-v`  

This is also the default 'motion' when going down the last visible line in the current frame. This will be one setting I will change as soon as possible. I do not like the jumpiness. I want the lines to scroll smoothly.  

- Move text under cursor: `C-l`  

This will move the text to the top, bottom and center of the screen, respectively. This mainly helps 'refocusing' the window when moving up and down with `C-v` and `M-v`.  

- Move cursor one character **forward**: `C-f`  
- Move cursor one character **backward**: `C-b`  
- Move cursor one line up (go to **previous** line): `C-p`  
- Move cursor one line down (go to **next** line): `C-n`  

Basic movement, indeed.  

- Move cursor one word **forward**: `M-f`  
- Move cursor one word **backward**: `M-b`  

This is my default way of moving around inside a file, besides 'movement by search'.    

- Move cursor to beginning of line (German: **Anfang**): `C-a`  
- Move cursor to end of line (German: **Ende**): `C-e`  

I knew those from the shell.  

- Move cursor to beginning of sentence (**Anfang**): `M-a`  
- Move cursor to end of sentence (**Ende**): `M-e`  

The location of the cursor in the text is also called 'point'. I'll try to use this term from now on.  

- Go to beginning of file: `M-<`  
- Go to end of file: `M->`  

## Delete, kill, yank and mark  
In Emacs, there is a difference between `kill` and `delete`. The former erases the line/string/character, but makes it `yankable`, which means it can be pasted again. This is a bit confusing for vim users, because `yank` means copy here, not paste.  

- Delete character before cursor: `<DEL>`  
- Delete next character after cursor: `C-d`  

Those will make the deleted characters not `yankable`.  

- Kill word before the cursor: `M-<DEL>`  
- Kill word after the cursor: `M-d`  
- Kill from the cursor position to end of line: `C-k`  
- Kill to end of current sentence: `M-k`  

Those make the deleted lines/string `yankable`.  

- Mark lines and press `M-w`  

Copy/kill without actually killing.  

- Yank last killed characters: `C-y`  
- Press `C-y` and then cycle with `M-y`.  

To cycle through the killed characters/lines  

- Visually mark lines: `C-<SPC>`  

Mark to kill.  

- Undo: `C-/`  

This is also a setting which needs configuring.  

## Buffers
When opening a file inside Emacs, it creates a buffer for this file. This buffer stays open until Emacs gets closed or the buffer itself gets killed. This makes it easy to jump between different files, even when the file itself got 'closed'.  

- Save current file: `C-x C-s`  
- Find file (open for editing): `C-x C-f`  

This will open the chosen file inside a new buffer.  

- Show all open buffers: `C-x C-b`  

One can select one of the buffers and press Enter to open this buffer.  

- Switch to buffer: `C-x b`  

With this one can start typing the buffer name and use <TAB> for auto-completion.  

There are also special buffers:  

- `*Buffer List*`, which contains the buffer list, obviously  
- `*Messages*`, contains the messages that have appeared on the bottom line during your Emacs session  

To save the edited files inside a buffer, one can type `C-x s`, which asks you about each buffer that need saving. 

## eXtended commands
Emacs has a lot of commands. A lot of them do not come with a keybinding out-of-the-box. So there are two ways of invoking these commands:  

- `C-x` **Character eXtend**: Followed by one character  
- `M-x` **Named command eXtend**: Followed by a long name  

So the first type is invoked by a chain of keybindings, the latter by pressing `M-x` and typing out the command.  

## Cancel a (running) command  

- Cancel a running or not yet invoked command: `C-g`  

## Mode line  
The line immediately above the echo area is called the "mode line". The mode line says something like this:

` -:**-  TUTORIAL       63% L749    (Fundamental) `  

This indicates if the current file has unsaved changes `**-`; this will be all dashes if it has not. The next part is the name of the currently active file, in this case it is `TUTORIAL`.  

The 63% indicates the current position in the active file. It will say `Top` if the top of the file is seen in the buffer and will say `Bot` if the opposite is the case. If the buffer is so small that the whole content fits one screen, it will say `All`.  

The `L` indicates the current line.

## Major modes
The part inside the parentheses indicates which major mode we are currently in. A major mode tells Emacs how to handle this specific buffer. Some examples are `Lisp mode`, `Text mode` or `Python mode`. All these just tell Emacs how to handle indentation, auto-completion and the like.  

Only one major mode can be active at any given time. To view documentation on the current major mode, type `C-h m`.

## Minor modes
Minor modes are specific 'nuances' of a major mode. There can be one, multiple or no minor modes at all at any given time.

An example, which is given in the tutorial is `Auto Fill mode`. It makes Emacs break the line in between words when the maximum number of characters per line are crossed.  

## Search  
- Search forward: `C-s`  
- Search backward: `C-r`  
The typed word is searched and displayed on the fly.  

## (Multiple) frames  

- Split horizontally: `C-x 2`  
- Split vertically: `C-x 3`  

To scroll the other, non-active window: `C-M-v` and `C-M-S-v`, respectively.  

- Kill the currently active window: `C-x 0`  
- Kill all other windows beside the active one: `C-x 1`  
- Move cursor to next frame: `C-x o`
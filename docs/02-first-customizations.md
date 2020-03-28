# First customizations

As stated earlier I wanted to tone down the customizing and tweaking to a bare minimum. In addition to that, I want to research exactly what the changes do and how they change Emacs default behavior.  

## init.el

When starting up, Emacs looks in specific places for its config file. These are:

- `~/.emacs`
- `~/.emacs.el`
- `~/.emacs.d/init.el`
- `~/.config/emacs/init.el` (starting with Emacs 27)  

Placing the config into `~/.emacs.d/init.el` is generally preferred.  

- First reason for that is that because of the `.el` ending Emacs automatically interprets the file as an Emacs Lisp file, and because of that, when editing the file Emacs automatically uses its Elisp major mode.  
- Second reason is that other than `~/.emacs.el` - which also has the `.el` ending and also has the same benefit as stated in reason 1 - `init.el` resides in a dedicated directory. So one can put all Emacs related files and directories into one place and keep everything nice and tidy.

So from now on I will assume that the reader's config is located at `~/.emacs.d/init.el`, where my own config resides.

## Intro to Lisp

The whole init file is written in Emacs Lisp. So one is actually writing code to configure Emacs. Basically the syntax of an expression looks like this (this is the example the [official Emacs documentation](https://www.gnu.org/software/emacs/manual/html_node/emacs/Init-Syntax.html#Init-Syntax) uses, which I highly recommend):

`(setq fill-column 60)`  

As the name `LISP`, which is an abbreviation for `LISt Processor`, indicates everything in Lisp is a list, which is indicated by the parentheses. Next, `setq` is the name of the called function, with `fill-column` being a variable and `60` being the assigned value of the variable. Constants in Emacs can be of type  

- number
- string
- `t` (True)
- `nil` (False)
- another Lisp object (indicated with a single `'` in front of it)

With `setq` one can set variables globally, most of the time. Some variables will be set as `buffer-local` variables, so they are just available inside the current buffer. So to make these variables globally available, one has to set them via `setq-default`. Also, what confused me a bit in the beginning was the documentation speaking of `symbols` - a symbol is just an object with a name. 

After making everything a bit clearer, I hope, let's start customizing Emacs!

## Customizing Emacs

### Visual declutter 

First, I want to get rid of the scroll, menu and tool bar and I do not want the cursor to be blinking. Those actually are globally enabled minor modes, so we do not use `setq`, we just disable them via:   

```
(menu-bar-mode -1)
(tool-bar-mode -1)
(scroll-bar-mode -1)
(blink-cursor-mode -1)
```

Notice that we are using `-1` instead of `nil`, because `nil` equals to no set and this in return means the modes will be still enabled.

### Startup screen

I do not want to see the splash screen every time I start Emacs, I want to see an empty `scratch buffer`. The scratch buffer always automatically starts when starting Emacs. It is a buffer which is in Elisp major mode from the get-go and is meant to quickly jot down something or try out an Elisp function.  

To have the current buffer be the `scratch buffer` and to disable the startup message it always contains, add this to your `init.el`. 

```
(setq inhibit-startup-screen t
      initial-scratch-message "")
```

### Font

I **really** like `IBM Plex Mono`. Feel free to use any other font (you should try `IBM Plex Mono`, though).

One changes the default font to use in all future frames like that:

```
(add-to-list 'default-frame-alist
    '(font . "IBM Plex Mono 12"))
```

Let's look a little closer at what that code block does.

It calls the function `add-to-list` with the argument `'default-frame-alist` which is a symbol (object) containing multiple `alists` which is short for `Association List`, which is just a key value pair. So with this we set the key `font` to the value `"IBM Plex Mono 12"`.

`add-to-list` goes through the whole list and, if the element is not yet set, will add it to the top of the list. Because of this it avoids duplicates but it also means when going through a big list the process will be expensive computation-wise. `'default-frame-alist` contains all the settings regarding the Emacs frames, e.g. height and width of the initial frame. 

### Line numbers

Next I want line numbers to be displayed, but relatively to where the cursor currently is. To do this, I put this into my config:

```
(setq display-line-numbers-type 'relative)
(global-display-line-numbers-mode 1)
```

This sets the variable `display-line-numbers-type` to `'relative`, which `global-display-line-numbers-mode` takes as an argument.  

### Show keystrokes faster  

I want to change the time it takes for Emacs to show which keys I pressed. The default is set to 1 second. I want it to be instantaneous. 

```
(setq echo-keystrokes 0.1)
```

### Disable audio

I also want to disable the pesky ring bell, which Emacs uses to indicate an error made. 

```
(setq ring-bell-function 'ignore)
```

This will set the variable `ring-bell-function` to use the function `'ignore` which just does nothing and return `nil`.There is also the possibility to make Emacs flash the screen, but I want none of that.  

### Show matching parentheses

Showing matching parentheses makes coding easier. This activates the minor mode `show-paren-mode` globally.

```
(show-paren-mode 1)
```

### Backups and autosaves

Emacs has the concept of backups and autosaves, which by default are more annoying than helpful to me. 

Backups are being created when the currently active file is saved for the first time. Emacs then either creates a copy of the file, or it renames the file and then creates a new buffer with the new content. 

The problem with this functionality is that the backup itself never gets deleted. So in the end, you have those backups lying all over the place. So I want to turn that off.

Also, Emacs creates autosaves when editing a file. Again, I do not like that behavior. The last line of code hinders Emacs to create the directory `auto-save-list`.

```
(setq make-backup-files nil)
(setq auto-save-default nil)
(setq auto-save-list-file-prefix nil)
```

### Tabs are evil

I want Emacs to insert spaces when indenting. Notice the `setq-default` to make this setting global.

```
(setq-default indent-tabs-mode nil)
```

### y-or-n
Instead of wanting me to type out yes or no, I want to just use y or n. `fset` sets a new function definition for a symbol, in this case `'yes-or-no-p` to `'y-or-n-p`.

```
(fset 'yes-or-no-p 'y-or-n-p)
```

### Auto-completion

Emacs has a builtin auto-completion mode, `ido-mode`. This shows existing files and buffers when searching for them with `C-x C-f` or `C-x b`.

```
(ido-mode 1)
```

## Side note  

There are other kind of init files which I will not focus in this chapter. You can read about them [here](https://www.gnu.org/software/emacs/manual/html_node/eintr/Site_002dwide-Init.html).  

Also, in the future I will list all topics I want to research for the chapter here.

### Research  

![Difference between push and add-to-list](https://emacs.stackexchange.com/questions/7389/whats-the-difference-between-push-and-add-to-list/7392)
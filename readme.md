---
author:
- gitten
title: Ur widget are belong to
type: Activity
---

Summary
=======

Intro activity for console applications using Urwid.

Objective
=========

First run through the urwid intro to build a little familiarty with the
library, then try to complete the main task by end of class.

Requirements
============

-   Shell terminal
-   `urwid`, library for console applications
-   Affection for musty old memes!

Tasks
=====

`urwid` intro
-------------

### Initial setup for activity

1.  Set up enviornment

    ``` {.bash}
    mkdir urwid; cd urwid
    virtualenv -p python3 env/
    env/bin/python -m pip install urwid
    touch scratch.py
    ```

2.  Add the following to your scratch.py file

    ``` {.python}
    import urwid

    markup = "ALL YOUR BASE ARE BELONG TO US"

    # instantiate application widgets
    txt = urwid.Text(markup)

    # instantiate "topmost" widget container
    fill = urwid.Filler(txt, 'middle')

    # instantiate application loop
    app = urwid.MainLoop(fill)

    app.run()
    ```

3.  Run your scratch file with `env/bin/python scratch.py`. Success?
    Success! close the program with `Ctrl-c`.

4.  notes
    -   `txt` is the instantiation of the
        \~urwid.Text()\~[(doc)](http://urwid.org/reference/widget.html#text)
        widget.

    -   \~urwid.Filler()\~[(doc)](http://urwid.org/reference/widget.html#filler)
        is called the "topmost" widget. It is the main container that
        holds all the application widgets.

        -   The second argument, \~'middle'\~ is the vertical alignment
            optional argument, the docs show that \~'middle'\~ is the
            default and there are three other possible settings.

    -   `urwid.MainLoop()` is an object class that handles the main
        application loop, the 'topmost' widget is passed as the only
        argument in this example.

### Global Interupt

1.  Lets make the application quit in a more user friendly way by adding
    a key interupt to exit the application. Create the following
    function definition above your widgets.

    ``` {.python}
    def exit_on_q(key):
        if key in ('q', 'Q'):
            raise urwid.ExitMainLoop()
    ```

2.  now lets add the `exit_on_q` function to the instantiation of our
    `MainLoop()`

    ``` {.python}
    loop = urwid.MainLoop(fill, unhandled_input=exit_on_q)
    ```

3.  notes
    -   The `unhandled_input` optional in MainLoop() handles all other
        events not managed by the application widgets. in this case, our
        only widget does not handle any events.

### Display Attributes and Decoration Widgets

1.  Lets create a `palette` for our small application. A palette is
    python list of `Attributes`. Each attribute is usually a tuple of
    strings of the form:

    ``` {.python}
    ('your_attribute_name', 'foreground_color', 'background_color' )
    ```

    Add the following above your widgets:

    ``` {.python}
    palette = [('banner', 'black', 'light gray'),
               ('streak', 'black', 'dark red'),
               ('background', 'black', 'dark blue')]
    ```

2.  Decoration Widgets are special widgets that wrap our application
    widgets. so many widgets! We will use the Decoration Widget
    `urwid.AttrMap()`
    [(docs)](http://urwid.org/reference/widget.html#attrmap). This wraps
    our application widgets with our pre-defined attributes from our
    `palette`. update your scratch application with the following
    starting with `markup`:

    ``` {.python}
    markup = ('banner', "ALL YOUR BASE ARE BELONG TO US")

    txt = urwid.Text(markup, align='center')
    txt_with_color_band = urwid.AttrMap(txt, 'streak')
    fill = urwid.Filler(txt_with_color_band)
    decorated_fill = urwid.AttrMap(fill, 'background')
    loop = urwid.MainLoop(decorated_fill, palette, unhandled_input=exit_on_q)

    loop.run()
    ```

3.  Play around with this for a bit and try to build up an intuition
    about how things are working. If you wish to change colors the key
    words can be found in the docs
    [here](http://urwid.org/manual/displayattributes.html#foreground-background).

### Show me what you got!

All ur widgets! They belong to us! Build us something interesting based
on the classic meme, "ALL YOUR BASE ARE BELONG TO US". We suggest you be
mindful of the process you are using to design your application. It
might be helpful to apply something like the "informal process"
discussed previously.

YOu mUst satisfy our tHirst for humOr and mehmehs or else!
![](https://media.giphy.com/media/26DOs997h6fgsCthu/giphy.gif)

Resources
---------

-   [urwid tutorial](http://urwid.org/tutorial/index.html)
-   [urwid manual](http://urwid.org/manual/index.html)
-   [urwid reference docs](http://urwid.org/reference/index.html)

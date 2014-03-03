IntermediateR
=============

2 day workshop material for "intermediate" R training with examples focusing on use for pharmaceutical sciences


Please feel free to contribute.

This is an amalgamation of material from around the web and books that have made understanding and using R easier. 

One of the biggest issues in diving into R is examples not targeted towards specific demographics - in my case, pharmaceutical sciences.

My goal is to rectify that by providing more relevant examples to the material at hand.

Navigating this repo:

Most of my writing is done in sublimetext (ST) 3. To facilitate tracking of issues, additions, etc (beyond the git repository) I use the sublimeTODO (ST2 only) plugin.

For ST3 a "new" official ST3 TODO package called [TodoReview](https://github.com/jonathandelgado/SublimeTodoReview) may be installed via package control (search TodoReview) and is actively being updated.

I have TODO patterns for the following:

* `BUG`
* `FIXME`
* `NOTE`
* `TOCHANGE`
* `TODO`

For example, if I want to add a `FIXME` not I could simply type:

`FIXME: example does not compile when .....`

To replicate my settings you can simply add the following information to your sublime settings (under Preferences):


```
    "todo":
    {
        "case_sensitive": true,
        "file_exclude_patterns":
        [
            "*.css",
            "*.po",
            "*.mo",
            "*.HTML",
            "*.sublime-settings",
            ".RData",
            ".Rhistory"
        ],
        "folder_exclude_patterns":
        [
            "static",
            "vendor",
            "tmp",
            ".Rproj.user"
        ],
        "patterns":
        {
            "BUG": "BUG[(]*.*[)]*:+(?P<bug>.*)$",
            "FIXME": "FIXME[(]*.*[)]*:+(?P<fixme>.*)$",
            "NOTE": "NOTE[(]*.*[)]*:+(?P<note>.*)$",
            "TOCHANGE": "TOCHANGE[(]*.*[)]*:+(?P<tochange>.*)$",
            "TODO": "TODO[(]*.*[)]*:+(?P<todo>.*)$"
        },
        "result_title": "TODO Results"
    },

```

Along with the following user key bindings (note keybindings only work with sublimeTODO (not TodoReview on ST3 at the moment))

```
{
  "keys": ["ctrl+shift+t"],
  "command": "todo",
  "args": {"open_files_only": false}
},
{
  "keys": ["ctrl+shift+alt+t"],
  "command": "todo",
  "args": {"open_files_only": true}
}

```

So the list of TODOs can be opened with `ctrl + shift + t` to see all TODO patterns and `ctrl + alt + shift + t` to see only TODO patterns with open files only.

The TODO list can also be found using the command pallete `ctrl + shift + p` + `todoresults`






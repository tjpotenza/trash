# `trash` - Delete a file or directory using the macOS system trash

## Why?

I've used a handful of CLI utilities that allow to use the MacOS trash utility, but wanted a version without any particular external dependencies and two main features: the ability to add a list of prohibited targets to avoid the occaisional accident, and for the deleted paths to be printed at runtime to make the scrolling through my terminal history a tiny bit easier.

## What?

Given the path to a file or dir, runs a few safety checks before using the MacOS system trash to delete it.  Will delete symlinks and not follow them, deleted files can be restored through the MacOS trash UI, and prints the absolute path of the file after deletion.  Also supports a dry-run mode when the environment variable TRASH_DRY_RUN="true".

This utility has a `prohibited_targets` list of paths that it will try to reject, to add a small guardrail against accidental deletion.  Additional directories or files can be added to this list at the top of this script's file.  The default list of prohibited targets is:

```
/
${HOME}
${HOME}/Desktop
```

## How?

`$ trash some-file.md `
```
💣 /Users/tjpotenza/Desktop/Projects/trash/some-file.md
```

`$ trash ~/Desktop`
```
❌ Safety checks prohibit deletion of [ /Users/tjpotenza/Desktop ].
```

`$ trash --help`
```
NAME
    trash - Delete a file or directory using the macOS system trash
    ...
```

`$ trash ./ghost.spooky`
```
❌ File or directory [ ./ghost.spooky ] not found.
```

## Disclaimer

I use this daily with great success, but admittedly haven't had the opportunity to test or validate that it behaves as expected beyond my fairly limited use cases, and am receptive to fixes for any bugs or issues that are discovered.

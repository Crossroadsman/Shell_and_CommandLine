watch
=====

`watch` is a handy tool to continually run another command at a specified interval.

Example:

```
watch -n 0.5 tree ~
```

This will run `tree` on the home directory every half second.




Note that watch is not installed by default on the Mac. It can be installed using 
[homebrew](https://github.com/Crossroadsman/ServerAdmin/blob/master/homebrew.md) by typing `brew install watch`.

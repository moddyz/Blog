---
layout: post
title: Poor man's environment variable management
---

Getting accustomed to the convenient developer tools at a VFX studio like Weta, then coming back home
to a fairly vanilla Ubuntu setup feels like a _serious downgrade_.

One major pain point is _environment management_.  

Being able to efficiently manipulate environment variables to test development projects is handy.

To make the process slightly less painful, and with the desire to stick to a terminal,
 introducing `appendEnv` and `prependEnv`:
```bash
prependEnv() 
{
    if [ $# -ne 2 ]
    then
        echo "usage: prependEnv <ENV_VAR> <ENV_VALUE>"
    else
        ENV_VALUE=`printenv $1`
        export $1="$2${ENV_VALUE:+${ENV_VALUE}:}"
    fi
}

appendEnv() 
{
    if [ $# -ne 2 ]
    then
        echo "usage: appendEnv <ENV_VAR> <ENV_VALUE>"
    else
        ENV_VALUE=`printenv $1`
        export $1="${ENV_VALUE:+${ENV_VALUE}:}$2"
    fi
}
```

These are bash aliases which can be slotted in your `~/.bash_aliases` file.

It's very simple - but an incremental step up from manually setting variables in many contexts.

You can find the up-to-date source in [this file](https://github.com/moddyz/UnixConfig/blob/master/.bash_aliases).

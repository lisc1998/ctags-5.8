# ctags-5.8
## fix ctags mask error
### make error example
```c
In file included from main.c:62:
/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/include/dirent.h:80:2: error: use of undeclared identifier 'unused'
        __unused long   __padding; /* (__dd_rewind space left for bincompat) */
        ^
/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/include/sys/cdefs.h:161:40: note: expanded from macro '__unused'
#define __unused        __attribute__((__unused__))
                                       ^
./general.h:60:37: note: expanded from macro '__unused__'
# define __unused__  __attribute__((unused))
                                    ^
1 error generated.
make: *** [main.o] Error 1
```

### modify general.h file

```c
 56 /*  This is a helpful internal feature of later versions (> 2.7) of GCC
 57  *  to prevent warnings about unused variables.
 58  */
 59 # define __unused__
 60 #if (__GNUC__ > 2  ||  (__GNUC__ == 2  &&  __GNUC_MINOR__ >= 7)) && !defined (__GNUG__)
 61 //# define __unused__  __attribute__((unused))
 62 # define __printf__(s,f)  __attribute__((format (printf, s, f)))
 63 #else
 64 //# define __unused__
 65 # define __printf__(s,f)
 66 #endif
 ```
## using ctags

add **alias ctags="`brew --prefix`/bin/ctags"** in ~/.zshrc
source ~/.zshrc

add **let Tlist_Ctags_Cmd="/usr/local/bin/ctags"** in .vimrc



---
title: Gomoku in Windows command line
date: 2017-10-12 21:00:00 +0100
categories: [programming]
tags: [games]
---

Windows command line is probably the most boring part of Windows system. I was thinking if I could write some funny program running in command line. I started experimenting with my favorite game - gomoku. Finally I created very simple command line version of gomoku. Algorithm is my own so it is not so strong but still it is able to win.

Let's try it out. First you will need to install c compiler for Windows. Probably the best one will be free [MinGW](https://www.mingw-w64.org/) compiler including `make` utility.

Clone project from GitHub

```
git clone https://github.com/oldcompcz/piskworks Piskworks
cd Piskworks
```

and compile it

```
make -f Makefile.gcc pisk_con
```


![Compile](/assets/gfx/piskworks/compile.png){: w="662" h="383" }

this will create `pisk_con.exe`.

Now you can run it and try it out.

![Game over](/assets/gfx/piskworks/game-over.png){: w="662" h="383" }

Gomoku is written in plain ISO C so it is possible to compile it and run it under Linux/Unix and even it is possible to build it for some old 8-bit computers. For more information see `README.md` file on [GitHub](https://github.com/oldcompcz/piskworks).

---
layout: post
title:  "Welcome to Jekyll!"
date:   2016-12-09 20:48:13 -0500
categories: arm
---
You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

```nasm
#define sfr_b(x)
#define sfr_w(x)
#define sfr_a(x)
#define sfr_l(x)
#include "msp430.h"
#define WD_FLAGS WDTPW|WDTHOLD

#define PC r0
#define SP r1
#define SR r2

_start:
    mov.w         #__stack,SP
stopWDT:
    mov.w        #WD_FLAGS, &WDTCTL
    bis.b         #1, &PADIR_L
    bis.b        #1 << 7, &PBDIR_H

    bic.b        #1, &PAOUT_L
    bic.b        #1 << 7, &PBOUT_H
loop:
    xor.b         #1, &PAOUT_L
    xor.b        #1 << 7, &PBOUT_H
    mov.w        #0xffff,SP
delay:
    dec.w        SP
    tst.w        SP
    jeq            loop
    jmp            delay
    nop

.section ".resetvec","ax",@progbits
          .word _start            ;0xfffe (RESET_VECTOR)

          .end
```

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/

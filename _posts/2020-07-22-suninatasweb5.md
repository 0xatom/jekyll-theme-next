---
title: SuNiNaTaS - Web 5
description: My writeup on web 5 challenge.
categories:
 - suninatas
tags: suninatas javascript obfuscated
---

![](https://i1.daumcdn.net/thumb/C264x200/?fname=https://t1.daumcdn.net/cfile/tistory/99DE7733599504E81D)

Hi all, let's pwn the 5 web challenge. This challenge was interesting.

You can start pwning there > [SuNiNaTaS](http://suninatas.com/){:target="_blank"}

## Solution

The challenge wants from us to check the key value:

![](https://i.imgur.com/AGMeSIQ.png)

If we check the source code we can see this in the end:

```
<!--Hint : 12342046413275659 -->
```

I tried to input this but nothing. Source code has a weird looking javascript code:

![](https://i.imgur.com/LNUggPE.png)

With my experience i can understand that this is obfuscated javascript code. (Obfuscator makes javascript code harder to read) We need to use a deobfuscator to get the clean code, i always use this one [de4js](https://lelinhtinh.github.io/de4js/)

![](https://i.imgur.com/NWkKcon.png)

We can see a "packer" in function, we need to use the packer option in the deobfuscator.

![](https://i.imgur.com/ls8vhaC.png)

We have the clean code:

```js
var digitArray = new Array('0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f');

function PASS(n) {
    var result = '';
    var start = true;
    for (var i = 32; i > 0;) {
        i -= 4;
        var digit = (n >> i) & 0xf;
        if (!start || digit != 0) {
            start = false;
            result += digitArray[digit]
        }
    }
    return (result == '' ? '0' : result)
}
```

We need to enter the comment string in PASS function, we can simply use the console from developer tools.

![](https://i.imgur.com/uN16SE7.png)

Let's enter this & we have the authkey: `Unp@cking j@vaScript`

![](https://i.imgur.com/ciX6PrC.png)

Bingo!

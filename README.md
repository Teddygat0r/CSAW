# CSAW

Ctf At: https://ctf.csaw.io/

## widthless

**Challenge Link**

Welcome to web! Let's start off with something kinda funky :)
http://web.chal.csaw.io:5018

**Solution**

When we first go to the website, we don't see anything out of the ordinary.  When we try to input anything into the `Signup for my newsletter`
input box, it doesn't let us input anything.  However, when we inspect element, we see a comment saying `zwsp is fun`, and a bunch of html character
codes at the bottom.

```&#8203;&#8203;&#8203;&#8203;&lrm;&rlm;&lrm;&#8203;&#8203;&#8203;&#8203;&zwnj;&zwj;&rlm;&#8203;&#8203;&#8203;&#8203;&lrm;&zwj;&rlm;&#8203;&#8203;&#8203;&#8203;&lrm;&zwj;&zwj;&#8203;&#8203;&#8203;&#8203;&rlm;&rlm;&#8203;&#8203;&#8203;&#8203;&#8203;&rlm;&lrm;&zwnj;&#8203;&#8203;&#8203;&#8203;&lrm;&#8203;&zwj;&#8203;&#8203;&#8203;&#8203;&zwj;&rlm;&zwj;&#8203;&#8203;&#8203;&#8203;&lrm;&#8203;&lrm;&#8203;&#8203;&#8203;&#8203;&zwnj;&rlm;&lrm;&#8203;&#8203;&#8203;&#8203;&lrm;&zwj;&lrm;&#8203;&#8203;&#8203;&#8203;&rlm;&rlm;&zwj;&#8203;&#8203;&#8203;&#8203;&zwj;&rlm;&rlm;&#8203;&#8203;&#8203;&#8203;&rlm;&#8203;&zwj;&#8203;&#8203;&#8203;&#8203;&lrm;&#8203;&zwj;&#8203;&#8203;&#8203;&#8203;&zwj;&#8203;&zwnj;&#8203;&#8203;&#8203;&#8203;&rlm;&zwj;&zwnj;&#8203;&#8203;&#8203;&#8203;&zwj;&zwj;&zwnj;&#8203;&#8203;&#8203;&#8203;&zwnj;&zwj;&rlm;```

These character codes happen to be the character codes of zwsp(Zero width space) characters.  These characters can be used in steganography,
so we assume we have to decode it.  Fortunately for us, theres this very nice website at

```
https://offdev.net/demos/zwsp-steg-js
```

that will let us decode these characters hidden in text.  We go to the source code, and copy paste it into the decoder, to get

```b'YWxtMHN0XzJfM3o='```
Which is `alm0st_2_3z` in base 64.

If we then input this into the `Signup for my newsletter` box, we get `/ahsdiufghawuflkaekdhjfaldshjfvbalerhjwfvblasdnjfbldf/<pwd>`

This is a link to the next page.  Replace `<pwd>` with `alm0st_2_3z`.
<br /><br />
Once we are at the next page, we check the source code of the website.  This time, we see that the zero width space characters are seperated throughout the website.  This doesn't
affect us, as if we do the same thing as before, we get `755f756e6831645f6d33` which is `u_unh1d_m3` in hex.  We put this into the new input box to get a link to the flag at:

```http://web.chal.csaw.io:5018//19s2uirdjsxbh1iwudgxnjxcbwaiquew3gdi/alm0st_2_3z/u_unh1d_m3```

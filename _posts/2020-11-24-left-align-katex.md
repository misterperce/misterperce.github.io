---
layout: post
title: Left Align LaTeX
---

This is kind of silly, but as I have been putting together my [multivariable calc notes/cheatsheet](/multivar), Kramdown's default LaTeX renderer, $${\KaTeX}$$, by default centers any $${\KaTeX}$$ written without text surrounding it (i.e. it handled inline fine, but any non-inline $${\KaTeX}$$ automatically became centered display $${\KaTeX}$$). And I wanted it to be left-aligned.

I went through a lot of documentation to see how I could adjust my `_config.yml` to evoke something like $${\KaTeX}$$'s `fleqn` option[^1] but had no success. Ultimately, adding this to my custom CSS worked for me:

```css
.katex-display>.katex {
	display: block;
	text-align: left !important;
	white-space: nowrap
}
```

I figured this out by:
* Looking at the $${\KaTeX}$$ CSS link: [https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css](https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css)
* Pasting its contents into [https://www.freeformatter.com/css-beautifier.html](https://www.freeformatter.com/css-beautifier.html) so I could actually read it
* And then Ctrl+F'ing for "center" and grabbing the relevant section
* Revising it to "left" :smirking-face:

&nbsp;

Here are some really nice posts that I enjoyed reading but did not solve my problem:
* [https://cullaloe.com/render-latex-in-jekyll/](https://cullaloe.com/render-latex-in-jekyll/)
* [https://xuc.me/blog/katex-and-jekyll/](https://xuc.me/blog/katex-and-jekyll/)
* [https://gendignoux.com/blog/2020/05/23/katex.html](https://gendignoux.com/blog/2020/05/23/katex.html)

[^1]: See [https://katex.org/docs/options.html](https://katex.org/docs/options.html)

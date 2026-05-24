+++
title = "On Typst"
date = 2026-05-24
+++

Around more than a year ago, I had to submit my lab practical files. In my university, they are submitted as physical prints. Since I needed to produce PDFs, I did what a normal person would obviously do: I opened a GUI text editor, LibreOffice Writer because I use Linux (Arch BTW). And it was a horrible experience trying to type and format text that had a lot of code in it.

I am not saying LibreOffice is a bad tool; it's actually a fantastic open-source project that offers a pretty close experience to MS Word in a Linux environment. A few reasons listed below made my experience not so good:

* I had to use the mouse a lot (I knew shortcuts, but I was a newbie to LibreOffice)
* To keep the document consistent, I had to put in a lot of manual effort
* There is no good way to insert raw code without breaking its formatting
* Lack of Vim motions (I know I am asking too much, but yeah, it's a nice-to-have feature and makes text editing much faster)
* Images are horrible to deal with

I have a gripe with GUI tools: usually there is no single way of doing things. Since no explicit training is required to use GUI tools, users often end up using less-recommended methods, like inserting a lot of line breaks instead of using page breaks.

Somehow I managed to format the files and submit them. But I was still searching for a tool that fit my needs. Around that time I was introduced to LaTeX through Luke Smith's YouTube channel. And man, I was so blown away seeing a program where I could edit text using Neovim, use custom automation, format raw code with syntax highlighting, and even draw diagrams and graphs using code.

So I installed and set up LaTeX with Neovim and Zathura. After playing around with it for some time, it wasn't as intuitive as I initially thought. Here are some problems I encountered while using LaTeX:

* The package system is a mess. I even considered using a Docker container to isolate the packages instead of bloating my main system.
* LaTeX lacks a good set of defaults. Yeah, it's highly customizable, but customizing everything takes time.
* The syntax is too... how do I say it... too descriptive. For example, using `\section{}` for a level-1 heading. I think it's because of Donald Knuth's [Literate Programming](https://en.wikipedia.org/wiki/Literate_programming) philosophy.
* Compilation is noticeably slow, and so is the preview.

Seasoned LaTeX users may argue that you encounter these problems when using LaTeX for cases it wasn't really intended for. Maybe they are right.

I needed a program that could replace GUI word processors for me. I needed something that I could use to quickly write things down and compile a decently formatted PDF.

So the search went on, and then I found Typst (I don't remember where). I installed and set up Typst in Neovim with the `typst-preview.nvim` plugin.

The first thing I noticed was how fast the preview was. After playing around with Typst for a little while, I realized it offered pretty much everything I wanted:

* Fast preview
* Markdown-like syntax
* Good defaults (for example, default fonts that remain readable when printed on modern printers)
* Vim support
* Easy yet powerful scripting
* Ability to use fonts installed on my system
* Default auto-pairing of inverted commas (I don't know why this isn't default in LaTeX, or at least why there isn't a flag or config option to enable it)
* Built-in basic features that required external packages in LaTeX
* Consistent formatting with pretty much no manual effort

I used Typst to typeset lab files, generate bulk documents, write letters, create resumes, reports, casual lists, etc., and Typst never seemed incapable.

It's been about a year now, and I never looked for an alternative. It may not be as powerful or customizable as LaTeX, but for me it was the LibreOffice Writer/Word replacement I was looking for. I even managed to get my friends to use Typst, and now they hate using GUI-based text editors.

If anyone is reading this article, consider this the sign you may or may not have been looking for to try Typst.

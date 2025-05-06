---
layout: post
title: Created First Ever Windows Executable Software in 2 Hours
date: 2025-05-06 12:55
author: har-singh
comments: true
categories: [blog]
---

For years, I used **PDFsam** on Windows to split or merge PDF files. It was a no-nonsense, solid tool. I discovered it long ago when looking for a free utility to extract or add pages from PDFs. Back then, PDFsam was simple freeware. I still have version 2.2.2, while the latest is 6.0.2. Unfortunately, when I tried running my old version on my current laptop, it required a Java Virtual Environment installation first. My current laptop didn’t have it installed, and I didn’t feel like jumping through hoops.

At times, I resorted to bash commands to get the job done. But this time I needed to split PDFs again, and I figured—why not just build a minimal tool myself?

I prompted ChatGPT with:

> "I want to create a simple windows application with GUI where a PDF document is uploaded and I can split or extract the pages."

Boom. It gave me Python code and instructions to package it as a Windows executable. I spun up a Windows 11 Pro VM in Azure, copy-pasted the code, ran the commands, and it generated the `.exe` file. Downloaded it to my laptop—it ran *and worked* on the first try. No errors. Just worked.

Next, I asked:

> "I have Python code to split the PDF document. It is very basic. Now I want that once uploaded it actually show the page representations. Representations could be simple emoji so if there are three pages there are three page icons."

Again, it delivered. Each page now showed as a basic icon.

Final prompt (for now):

> "Very good. Now how to make the icon selectable? User can select the icons and then extract the page. The output is the document with selected pages (icons)."

Result: success.

It’s basic, it works, and it’s my first real Windows executable built from scratch. You can check out the code here:
🔗 [https://github.com/har-singh/pdfgeek](https://github.com/har-singh/pdfgeek)

No bloated libraries. No installers. Just code, AI prompts, and a working tool.

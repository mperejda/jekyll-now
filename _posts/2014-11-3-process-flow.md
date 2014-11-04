---
layout: post
title: The Critical Path and Debugging
---

Becoming a master is challenging.

I'm starting to understand the fundamental building blocks that make up simple programs, web apps, and anything else programmable.

Once you know what tools you will need, time to start work. The only way to get better at hammering nails is to hammer nails.

The skills craftsman has many tools and must master them all to become competent. I argue the amateur developer has the same challenge as the apprentice learning blacksmithing.

[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/HGz2BVtvS5I/0.jpg)](http://www.youtube.com/watch?v=HGz2BVtvS5I)


Debugging is one of those skills that moves you forward. Your code will never be perfect. Ever. Then what does "getting better" look like?

Finding your mistakes with blazing speed, by-line, methodically. Then ship quality product. 

Debugging is not sexy and seems "meh" compared to the idea of becoming a "code ninja" that executes perfect logic with flawless syntax. In reality, impressive engineers are brilliantly effective at fixing their bugs before anyone even knows they exist.

Is the value proposition clear yet?

![alt text](http://pryrepl.org/images/pry_logo.png)

[Pry](prryrepl.org) and [debugger](https://github.com/cldwalker/debugger) are my go to combo for ruby. [App Academy](https://github.com/appacademy/prep-work/blob/master/mini-curriculum/README.md) has an excellent tutorial to get you started or you can jump to [Josh Cheek's](https://vimeo.com/26391171) overview of pry and it's functionality.

---

**Important For Loading Scripts w/ Pry**

Scenario: `require './method.rb'` in pry. Test a method. Method fails test.

When you edit your method.rb file and update in pry w/ `load './method.rb' ` the text shown by the debugger will NOT reflect your changes but WILL run the new code and pry will work accordingly (bug as of 11/2014). You'll need to reset pry and `require './method'` again if you want to get around this.

---

It takes time to learn these tools and you will make mistakes. Once you start to master them, they will save you an uncountable amount of time and shorten your development cycle. You can only move forward as fast as you can debug.

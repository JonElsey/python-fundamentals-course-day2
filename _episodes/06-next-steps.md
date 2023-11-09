---
title: Next steps
teaching: 20
exercises: 0
questions:
    - "Where can I go from here?"
    - "What other opportunities are available for me to learn more?"
    - "How do I start to think like a software developer (rather than a coder)?"
objectives:
    - "Knowing what best practices are when thinking about code (as opposed to just writing it!)"
    - "Determine where additional training materials can be found."
    
keypoints:
    - "Write lots of code!"
    - "Use the Internet, particularly StackOverflow, use my expertise and talk to one another about problems you are facing!"
    
---

# Things to try and think about when writing code

* Coding is difficult!
  
  If you get stuff wrong, that's OK! You will 100% write code that doesn't work, or has bugs in it. *This is normal!* I've been writing code in Python for 10 years and still get basic stuff wrong. 

* Don't get discouraged!

  The best thing to do is to have a go at solving the problem. Worst case - your code throws an error. Think about what is causing the error, solve it, and move onto the next one! Each time you solve an error, you will know what to do when it occurs again next time. See fixing problems as an opportunity for growth rather than something negative. 

* Break down problems into smaller ones

  Think like a scientist - if we see a big problem, it is often constructive to break it down into several smaller ones, then build them together to find the solution. As tempting as it is to write big long scripts with lots of repeated (read: copy and pasted) code, if you can, don't! Think about problems before you solve them - how can we decompose it into functions that solve one specific problem each, and then bring it all together?

This can be a huge time saver as well - often you'll write bits of code that solve similar problems - why not just re-use the same functions/code from your previous project? I have an ever-evolving list of useful functions I've written to solve specific (often menial) problems I often face when doing data analysis/visualisation.

* Be organised

A huge amount of overhead with software is maintenance - in scientific terms this might just mean coming back to code you wrote previously for a paper correction or something. So many times I've looked back at my own code and thought "what on Earth is this nonsense!". Writing logical code split into functions with *lots of comments* helps readability a ton. Also, use logical names and structures for everything. If your data analysis has a bunch of constants/data imports, keeping these at the top of scripts will help you to work out what they do much easier. Have different folders for different projects, so that you can navigate to the specific bit of code you were using easier. Name your scripts something meaningful too! You're not going to remember what "script.py" does in 6 months, but "west_africa_rainfall_analysis.py" might be more useful. This extends to variable names too! Avoid using names like "data" if possible - better to explicitly refer to what you're looking at (so something like "rainfall_data_in" for loading in a netCDF, then splitting this into variables like "lat", "long" and "rainfall").

* Write comments!

I mentioned this already but its so important it bears repeating - writing comments helps others to understand code you've written (without the benefit of having written it), but also helps you to work out what that bit of code you wrote days/weeks/months/years ago does a lot faster than actually reading the code. Try and have comments both at the top-level (what does this function do/what purpose does it serve?), and also perhaps for individual lines of code for tricks and things that may be a bit arcane to work out without context (e.g. if you are doing some kind of normalisation on your data).

* Don't reinvent the wheel!

Often, someone will have already solved the task you want to try and solve. It is often much better to use their solution! Search around for functions that do what you want (Numpy and the scientific computing library Scipy usually have you covered if its anything mathematical), or libraries if your problem is specific to your field of study!

* Don't worry about optimisation (yet)

When writing code, premature optimisation is the enemy! Write something that works first, then optimise the bits that are slow. Writing a data analysis script for 100000 different data files? Write something that works for 10 files first, see how fast it is, work out the bits that are slow, then scale. You can always ask me for help if speed is ever an issue. Most data analysis tasks can be run on personal computers. You may eventually run into problems that require High Performance Computing (often abbreviated HPC) - please get in touch if so!



# Additional training

ARCCA have some training courses available on their [website](https://arcca.github.io), which I recommend. They tend to run these a few times a year, or you can work through the material in your own time. 

ARCCA's courses (and indeed this one!) are based to various degrees on courses developed by an organisation called The Carpentries. You can find their software lessons [here](https://software-carpentry.org/lessons/). Additional lessons are available on the [Data Carpentries](https://datacarpentry.org/lessons/) website; these tend to focus on more specific but still potentially relevant things. These are also highly recommended! 

{% include links.md %}



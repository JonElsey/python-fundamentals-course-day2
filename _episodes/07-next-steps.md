---
title: Next steps
teaching: 40
exercises: 0
questions:
    - "Where can I go from here?"
    - "What are some useful tips and tricks to know when coding?"
    - "What other opportunities are available for me to learn more?"
objectives:
    - "Knowing what best practices are when thinking about code (as opposed to just writing it!)"
    - "Determine where additional training materials can be found."
    
keypoints:
    - "Write lots of code!"
    - "Use the Internet, particularly StackOverflow, use my expertise and talk to one another about problems you are facing!"
    
---

# Things to try and think about when writing code

* **Coding is difficult!**
  
  If you get stuff wrong, that's OK! You will 100% write code that doesn't work, or has bugs in it. *This is normal!* I've been writing code in Python for 10 years and still get basic stuff wrong. 

* **Don't get discouraged!**

  The best thing to do is to have a go at solving the problem. Worst case - your code throws an error. Think about what is causing the error, solve it, and move onto the next one! Each time you solve an error, you will know what to do when it occurs again next time. See fixing problems as an opportunity for growth rather than something negative. 

* **Break down problems into smaller ones**

  Think like a scientist - if we see a big problem, it is often constructive to break it down into several smaller ones, then build them together to find the solution. As tempting as it is to write big long scripts with lots of repeated (read: copy and pasted) code, if you can, don't! Think about problems before you solve them - how can we decompose it into functions that solve one specific problem each, and then bring it all together?

  This can be a huge time saver as well - often you'll write bits of code that solve similar problems - why not just re-use the same functions/code from your previous project? I have an ever-evolving list of useful functions I've written to solve specific (often menial) problems I often face when doing data analysis/visualisation.

* **Think logically/procedurally**

  Often your code will fail and you'll be unsure as to why. The computer will only ever execute the actions you write *exactly as you have written them*. Work through your code and try and work out what is happening to your variables at each step. 

* **Be organised**

  A huge amount of overhead with software is maintenance - in scientific terms this might just mean coming back to code you wrote previously for a paper correction or something. So many times I've looked back at my own code and thought "what on Earth is this nonsense!". Writing logical code split into functions with *lots of comments* helps readability a ton. Also, use logical names and structures for everything. If your data analysis has a bunch of constants/data imports, keeping these at the top of scripts will help you to work out what they do much easier.

  Have different folders for different projects, so that you can navigate to the specific bit of code you were using easier. Name your scripts something meaningful too! You're not going to remember what "script.py" does in 6 months, but "west_africa_rainfall_analysis.py" might be more useful. This extends to variable names too! Avoid using names like "data" if possible - better to explicitly refer to what you're looking at (so something like "rainfall_data_in" for loading in a netCDF, then splitting this into variables like "lat", "long" and "rainfall").

* **Write comments!**

  I mentioned this already but its so important it bears repeating - writing comments helps others to understand code you've written (without the benefit of having written it), but also helps you to work out what that bit of code you wrote days/weeks/months/years ago does a lot faster than actually reading the code.

   Try and have comments both at the top-level (what does this function do/what purpose does it serve?), and also perhaps for individual lines of code for tricks and things that may be a bit arcane to work out without context (e.g. if you are doing some kind of normalisation on your data).

* **Don't reinvent the wheel!**

  Often, someone will have already solved the task you want to try and solve. It is often much better to use their solution! Search around for functions that do what you want (Numpy and the scientific computing library Scipy usually have you covered if its anything mathematical), or libraries if your problem is specific to your field of study!

* **Don't worry about optimisation (yet)**

  When writing code, premature optimisation is the enemy! Write something that works first, then optimise the bits that are slow. Writing a data analysis script for 100000 different data files? Write something that works for 10 files first, see how fast it is, work out the bits that are slow, then scale. You can always ask me for help if speed is ever an issue. Most data analysis tasks can be run on personal computers. You may eventually run into problems that require High Performance Computing (often abbreviated HPC) - please get in touch if so!


  


# Tips and Tricks

These are some little things which you will likely pick up as you start to write more code. We have not necessarily used them in the earlier portions of the course to minimise cognitive load, but "in the wild" you will likely see people using these!

* Block comment in Jupyter Notebooks using Ctrl + / (or Cmd + / on Mac)

* Cut down on typing using the ``as`` keyword...

  When importing modules, you can use the ``as`` keyword to create a kind of shorthand. For example:
    ``import numpy as np``
  lets you type ``np.sum(wave_data)`` instead of ``numpy.sum(wave_data)``.

* ... or using the ``from`` keyword.

  You can also, if you are only importing specific parts of a module, use the ``from`` keyword. For example:

  ``from netCDF4 import Dataset``

  lets you type ``Dataset(wave_data)`` instead of ``netCDF4.Dataset(wave_data)``.

* Use ``help`` to get info on a function (or use Google)

  e.g. ``help(np.sum)`` (assuming the ``import numpy as np`` syntax from earlier)

* Use Conda environments!

  So far during this course, we have only used the "base" Anaconda environment. An environment is effectively like a fresh install of Python. This can be very useful when working with libraries, as often they will be dependent on other libraries; when one is updated it can cause everything to stop working, or perhaps two different libraries need two different versions of another library to work.

You can create a new Conda environment from the command line using:

``conda create --name <your_name_here> python``.

Or to create one with a specific version of python, in this case an environment called ``waves_project``:

``conda create --name waves_project python=3.9``.

This will create a blank slate Python, from which you can install libraries etc. again (you will need to install Jupyter notebook in this environment if you want to use these, via ``conda install jupyter``)
# Other useful libraries for scientific computing (useful to be aware of, although you likely won't use some of these until much later)

* Scipy - algorithms for scientific computing - useful for statistics, working with matrices, probability distribution functions, optimisation problems, interpolation/extrapolation and differential equations
* Scikit-image - Image processing
* Scikit-learn - Machine learning/data science - good at almost all standard ML tasks aside from deep learning/neural networks
* BeautifulSoup - web scraping, potentially really useful for data collection
* Dask - parallel computing
* Sympy - symbolic maths using Python! If any of you have used Mathematica, it has similar functionality. 

# Other languages that might be of interest

* R - also free, focused more on statistics/data manipulation, has similar functionality to Python in a lot of places but may be a little easier to use
* Matlab - University has a paid license, can be good for some specific tasks
* Fortran/C - used by people doing numerical modelling/number crunching, very hard to learn but necessary for some types of computing
* Julia - new upstart language, bridges the gap between the speed of Fortran and the library support/ease of use of Python

# Additional training

ARCCA have some training courses available on their [website](https://arcca.github.io), which I recommend. They tend to run these a few times a year, or you can work through the material in your own time. 

ARCCA's courses (and indeed this one!) are based to various degrees on courses developed by an organisation called The Carpentries. You can find their software lessons [here](https://software-carpentry.org/lessons/). Additional lessons are available on the [Data Carpentries](https://datacarpentry.org/lessons/) website; these tend to focus on more specific but still potentially relevant things. These are also highly recommended! 

Depending on your feedback, I may also offer more advanced courses in future.

# Things not covered here (which you may see out in the wild) - read this in your own time if interested!

* Using the command line

  While at first it is useful to run code in Jupyter notebooks or in Spyder, longer term it is very useful to get comfortable using the command line, particularly using the Bash shell (found on Linux/Mac). This will allow you to run your code in batch scripts, allowing for use on HPC systems, or just running lots of iterations of your code at once. ARCCA have some useful training on how to do this.

* Object oriented code
  
  A lot of code you will see may use what we call an ``object oriented`` approach. For example, instead of doing ``np.sum(array)``, you may see something similar to ``array.sum()``. We touched on this when working with our netCDF files - e.g. when loading in a netCDF using ``Dataset``, this is an object, which we operate on using the ``variables`` *method* to get e.g. our lat/long grids and our temperature fields from the CRU example. 

  This is something I may give a workshop on in future as it is a very useful way of thinking about code when writing your own - particularly for large-scale projects.
  
{% include links.md %}



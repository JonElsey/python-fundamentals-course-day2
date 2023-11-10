---
title: Working with netCDF files and creating animations
teaching: 60
exercises: 30
questions:
   
objectives:

    
keypoints:

---

### NetCDF files

What about data stored in other types of files? Scientific data is often stored in
[NetCDF](https://en.wikipedia.org/wiki/NetCDF) files.

NetCDFs are nice! They are *self-describing* - i.e. they are set up to contain both the data required, and any metadata that helps the user understand that data. They are often used to store large 3 (or greater) dimensional matrices or tensors, making them ideal for storing data on e.g. the vertical and horizontal structure of the atmosphere over long timescales. Data such as the [ERA5](https://www.ecmwf.int/en/forecasts/dataset/ecmwf-reanalysis-v5) climatological reanalysis are stored in netCDF - often with tens or hundreds of different atmospheric variables gridded at each temporal and spatial point. Such large datasets would be very unwieldy to work with in Numpy or even using Pandas, but netCDF has us covered. We will be looking a less complex dataset than this here - but the principles can be applied to using these datasets also.

Python has a library called ``netCDF4`` which is designed for operating with these files. 

We will again use data describing sea waves, but this time looking at a spatial map. This data set shows a static world map, containing data with the multi-year average wave climate. Again, hs_avg is the wave height in metres. But this time, the shape of the matrix is latitude x longitude

> ## Using other libraries
>
> For the rest of this lesson, we need to use a python library that isn't included in the default
> installation of Anaconda. There are various ways to doing this, depending on how you opened the Jupyter Notebook:
>
> If you're using Anaconda Navigator:
> - return to the main window of Anaconda Navigator
> - select "Environments" from the left-hand menu, and then "**base** (root)"
> - Select the Not Installed filter option to list all packages that are available in the environment’s channels, but not installed.
> - Select the name of the package you want to install. We want `NetCDF4`
> - Click Apply
>
> If you opened the Jupyter Notebook via the command line:
> - you'll need to close the Notebook (Ctrl+C, twice)
> - run the command `conda install netcdf4`, and accept any prompt(s) (`y`)
{: .callout}

~~~
import netCDF4 as nc
~~~
{: .language-python}

We can then import a netCDF file, and check to see what python thinks its type is:

~~~
globaldata = nc.Dataset("multyear_hs_avg.nc")
print(type(globaldata))
~~~
{: .language-python}

~~~
<class 'netCDF4._netCDF4.Dataset'>
~~~
{: .output}

We can use Matplotlib to display this data set as a world map. The data go from -90 degrees (south pole) to +90 degrees (north pole) in the y direction. In the x-direction the data go from 0 to 360 degrees East, starting at the Greenwich meridian. The white areas are land, because we have no data there to plot.

~~~
matplotlib.pyplot.imshow(globaldata["hs_avg"][0], extent=[0,360,-90,90], origin='lower')
matplotlib.pyplot.show()
~~~
{: .language-python}

![Global surface waveheight](../fig/global_surfaceu.svg)

NetCDF files can be quite complex, and normally consist of a number of variables stored as 2D or 3D arrays. `globaldata["hs_avg"]`
is getting a variable called *hs_avg*, which is of type `netCDF4._netCDF4.Variable` (the full list of variables stored can be listed with
`gdata.variables.keys()`). We can use the first element of `globaldata["hs_avg"]` to plot the global map using the `imshow()` function.
Although the type of this element is `numpy.ma.core.MaskedArray`, the `imshow()` function can natively use this variable type as input.

We then need to specify that the data axes of the plot need to go from 0 to 360 on the x-axis, and -90 to 90 on the y-axis. We also use
`origin='lower'` to stop the map being displayed upside down, because we want the map being plotted from the bottom-left, rather than the top-left 
which is the default for plotting matrix-type data (because this is where `[0:0]` normally is).

We can also add a colour bar to help describe the figure, with a little more code:

~~~
import mpl_toolkits

matplotlib.pyplot.figure()
ax = matplotlib.pyplot.gca()
im = ax.imshow(globaldata["hs_avg"][0], extent=[0,360,-90,90], origin='lower')

divider = mpl_toolkits.axes_grid1.make_axes_locatable(ax)
cax = divider.append_axes("right", size="5%", pad=0.05)

matplotlib.pyplot.colorbar(im, cax=cax)
~~~
{: .language-python}

Here, we don't need to use the `mpl_toolkits` library, but it's useful to help format the colourbar.

![Global surface waveheight with a colourbar](../fig/global_surfaceu-colourbar.svg)

{% include links.md %}


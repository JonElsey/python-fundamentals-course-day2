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
globaldata = nc.Dataset("cru_data.nc")
print(type(globaldata))
~~~
{: .language-python}

~~~
<class 'netCDF4._netCDF4.Dataset'>
~~~
{: .output}

We can look at what variables our netCDF contains by doing:

~~~
globaldata.variables.keys()
~~~
{: .language-python}

~~~
dict_keys(['lon', 'lat', 'time', 'tmp', 'stn'])
~~~
{: .output}

Here we can infer that we have three co-ordinates, longitude, latitude and time, and two variables 'tmp' and 'stn'. We can probably guess that 'tmp' is temperature, since we are looking at surface temperature data, but what is 'stn'? Let's check this out in more detail. We can do this using:

~~~
globaldata.variables['stn']
~~~
{: .language-python}

~~~
<class 'netCDF4._netCDF4.Variable'>
int32 stn(time, lat, lon)
    description: number of stations contributing to each datum
unlimited dimensions: time
current shape = (84, 360, 720)
filling on, default _FillValue of -2147483647 used
~~~
{: .output}

So we see that 'stn' is some extra data that is useful to understand the reliability of our temperature data. We can also see the shape of the data - ``(84, 360, 720)``. This gives us an indication of the co-ordinates - it is likely that 360 and 720 refer to latitude/longitude, which means we have 84 temporal points. Let's check using the ``.variables['var']`` syntax again:

~~~
globaldata.variables['time']
~~~
{: .language-python}

~~~
<class 'netCDF4._netCDF4.Variable'>
float32 time(time)
    long_name: time
    units: days since 1900-1-1
    calendar: gregorian
unlimited dimensions: time
current shape = (84,)
filling on, default _FillValue of 9.969209968386869e+36 used
~~~
{: .output}

Yes, this checks out. Our time array has a length of 84. But what does "days since 1900-1-1" mean for us? Let's have a look at the actual values in the dataset. We do this by adding a slice to what we put previously. Let's slice for all of the data in the array.

~~~
globaldata.variables['time'][:]
~~~
{: .language-python}

~~~
masked_array(data=[40557., 40587., 40616., 40647., 40677., 40708., 40738.,
                   40769., 40800., 40830., 40861., 40891., 40922., 40952.,
                   40982., 41013., 41043., 41074., 41104., 41135., 41166.,
                   41196., 41227., 41257., 41288., 41318., 41347., 41378.,
                   41408., 41439., 41469., 41500., 41531., 41561., 41592.,
                   41622., 41653., 41683., 41712., 41743., 41773., 41804.,
                   41834., 41865., 41896., 41926., 41957., 41987., 42018.,
                   42048., 42077., 42108., 42138., 42169., 42199., 42230.,
                   42261., 42291., 42322., 42352., 42383., 42413., 42443.,
                   42474., 42504., 42535., 42565., 42596., 42627., 42657.,
                   42688., 42718., 42749., 42779., 42808., 42839., 42869.,
                   42900., 42930., 42961., 42992., 43022., 43053., 43083.],
             mask=False,
       fill_value=1e+20,
            dtype=float32)
~~~
{: .output}

We could similarly do so for an arbitrary index, let's say the first one:

~~~
globaldata.variables['time'][0]
~~~
{: .language-python}

~~~
masked_array(data=40557.,
             mask=False,
       fill_value=1e+20,
            dtype=float32)
~~~
{: .output}

So our time data is a set of numbers, differing by 30 or 31. These must be monthly data then! But how can we get this into a nice format? Let's put this to one side a second and focus more on our temperature data.



~~~
matplotlib.pyplot.imshow(globaldata["hs_avg"][0], extent=[0,360,-90,90], origin='lower')
matplotlib.pyplot.show()
~~~
{: .language-python}

![Global surface waveheight](../fig/global_surfaceu.svg)



~~~

~~~
{: .language-python}

Here, we don't need to use the `mpl_toolkits` library, but it's useful to help format the colourbar.

![Global surface waveheight with a colourbar](../fig/global_surfaceu-colourbar.svg)

{% include links.md %}



# Visualizations and Word Clouds <a id="top"></a>

## Table of Contents

1. [Introduction](#intro)
    1. Last Week
        1. Data Science
        2. Python
            1. Data Types
            2. Methods
            3. Packages
    2. Visualization
        1. Common Graphs
        2. Packages
2. [Getting Started](#start)
3. [Choosing Colors](#color)
4. [Adding Labels](#labels)
5. [Summary](#sum)

### Introduction <a id="intro"></a>
Welcome to week 2! Last week we covered a lot. We started with an overview of data science, both from a career and work flow perspective and tehn continued on to cover the basic datatypes of python. Today, we are going to continue where we left off and take a further look into creating some stunning visuals!

#### Last Week

##### The Typical Data Science Workflow <a id="ds_workflow></a>
![](./images/data_science_lifecycle.png)
##### Python Data Types
![](./images/dataStruct.png)
##### Packages
We also saw how to load packages into python in order to use additional functions and methods stored within them.   
Recall:

#### Visualization

##### Common Graphs
![](./images/Data_Viz_Catalog.png)

##### Packages
* plotly
* matplotlib
* pandas (Primarily a spreadsheet [excel-like] package, but has some built in visualizations using matplotlib)
* folium
* seaborn (Makes everything prettier!)


```python
import pandas
travel_df = pandas.read_excel('./cities.xlsx')
cities = travel_df.to_dict('records')
cities[0]
```




    {'City': 'Solta', 'Country': 'Croatia', 'Population': 1700, 'Area': 59}



### Getting Started <a id="start"></a>

Let's pull in some data!

### Importing Modules
Technically we already did this (we imported the pandas package up above) but let's do it once again just as a reminder.  
This time we'll also **alias** the pandas package as **pd** while it may not seem like a lot saving those 4 letters typing will add up if we're using it frequently.


```python
import pandas as pd
```

#### Modules https://docs.python.org/2/tutorial/modules.html
Here's the official blurbs about Methods and Importing from python:

"If you quit from the Python interpreter and enter it again, the definitions you have made (functions and variables) are lost. Therefore, if you want to write a somewhat longer program, you are better off using a text editor to prepare the input for the interpreter and running it with that file as input instead. This is known as creating a script. As your program gets longer, you may want to split it into several files for easier maintenance. You may also want to use a handy function that you’ve written in several programs without copying its definition into each program.

To support this, Python has a way to put definitions in a file and use them in a script or in an interactive instance of the interpreter. Such a file is called a module; definitions from a module can be imported into other modules or into the main module (the collection of variables that you have access to in a script executed at the top level and in calculator mode)."


#### Packages (collections of Modules)  https://docs.python.org/3/reference/import.html
"It’s important to keep in mind that all packages are modules, but not all modules are packages. Or put another way, packages are just a special kind of module. Specifically, any module that contains a __path__ attribute is considered a package."  

#### Importing https://docs.python.org/3/reference/import.html
"Python code in one module gains access to the code in another module by the process of importing it. The import statement is the most common way of invoking the import machinery, but it is not the only way. Functions such as importlib.import_module() and built-in __import__() can also be used to invoke the import machinery."


```python
df = pd.read_excel('cities.xlsx')
df.head() #Preview the first 5 rows of the dataframe
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Country</th>
      <th>Population</th>
      <th>Area</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Solta</td>
      <td>Croatia</td>
      <td>1700</td>
      <td>59</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Greenville</td>
      <td>USA</td>
      <td>84554</td>
      <td>68</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Buenos Aires</td>
      <td>Argentina</td>
      <td>13591863</td>
      <td>4758</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Los Cabos</td>
      <td>Mexico</td>
      <td>287651</td>
      <td>3750</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Walla Walla Valley</td>
      <td>USA</td>
      <td>32237</td>
      <td>33</td>
    </tr>
  </tbody>
</table>
</div>



#### Common Pandas methods
* df.head() #Preview the first 5 rows of the dataframe
* df.head(10) #Preview the first 10 rows
* df.tail() #Preview the last 5 rows
* df.columns #Returns a list of the column names Notice that this is an attribute not a method/function; there are no parentheses
* df.info() #Return column names, length of dataframe and storage size info
* df[col] #Return a particular column of the dataframe where col is the name of the column
* df[col].value_counts() #Returns a frequency count of entries within the column in descending order
* df[col].unique() #Returns a list of unique entries within the column
* df[col].nunique() #Returns the number of unique entries within the column as an integer
* df[[cols]] #Returns the dataframe with only those columns indicated



```python
%matplotlib inline
```

## Making a Bar Chart
Let's make a bar chart of cities and their population.


```python
df['Population'].plot(kind='bar')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x11b925b00>




![png](output_10_1.png)


Hmmm, it would sure be nice to have the actual names of the cities on our graph!
To do this, we have to tell Pandas what feature we want to use as the **index** for the dataframe.
The index is shown on the left edge and can be thought of as the row names.


```python
df.set_index('City')['Population'].plot(kind='bar')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x112f9ab00>




![png](output_12_1.png)


Better. Let's also change this to a horizontal bar chart so that the cities are easier to read.


```python
df.set_index('City')['Population'].plot(kind='barh') #Notice barh instead of bar
```




    <matplotlib.axes._subplots.AxesSubplot at 0x11bbc0f60>




![png](output_14_1.png)


Great! I want to make my chart all orange though!

### Choosing Colors <a id="color"></a>
Here's a few helpful resources for getting started:  
http://colorbrewer2.org/#type=sequential&scheme=YlOrRd&n=3  
https://matplotlib.org/api/colors_api.html  


```python
df.set_index('City')['Population'].plot(kind='barh', color='Orange')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x11c35f6a0>




![png](output_17_1.png)


We can do way better then that though!  
Checkout what you can do with the **seaborn** package and their color palettes!


```python
import seaborn as sns
```


```python
sns.set_style("darkgrid") #Load in some snazzier visual settings to spice things upb
```

See https://seaborn.pydata.org/tutorial/aesthetics.html for all too many options


```python
df.set_index('City')['Population'].plot(kind='barh') #Same code, prettier graph thanks to Seaborn!
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a1e21fda0>




![png](output_22_1.png)



```python
sns.palplot(sns.light_palette((210, 90, 60), input="husl")) #Previewing a color scheme
```


![png](output_23_0.png)



```python
sns.palplot(sns.dark_palette("muted purple", input="xkcd")) #Another color scheme!
```


![png](output_24_0.png)



```python
sns.palplot(sns.color_palette("Paired")) #And another
```


![png](output_25_0.png)


Those purples were amazing! Let's incorporate them into our graph.


```python
dark_purples = sns.dark_palette("muted purple", input="xkcd")
df.set_index('City')['Population'].plot(kind='barh', color = dark_purples)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1a1e4e1438>




![png](output_27_1.png)


### Adding Labels <a id="labels"></a>

We need another module for this one. 


```python
import matplotlib.pyplot as plt
```


```python
#Same Initial Code
dark_purples = sns.dark_palette("muted purple", input="xkcd")
df.set_index('City')['Population'].plot(kind='barh', color = dark_purples)

#Now Add a title
plt.title('Cities by Population')

#Label the X-Axis
plt.xlabel('Population in Tens of Millions')
```




    Text(0.5,0,'Population in Tens of Millions')




![png](output_31_1.png)


#### Once more for good measure...
This time lets make everything bigger!


```python
#Same Initial Code
dark_purples = sns.dark_palette("muted purple", input="xkcd") 
df.set_index('City')['Population'].plot(kind='barh', color = dark_purples, figsize=(15,12)) #Bigger graph

#Now Add a title
plt.title('Cities by Population', fontsize=22)

#Label the X-Axis
plt.xlabel('Population in Tens of Millions', fontsize=16)

#Enlarge the Y-Axis Label
plt.ylabel('City', fontsize=16)

#Enlarge the City Names themselves
plt.yticks(fontsize=14)
```




    (array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11]),
     <a list of 12 Text yticklabel objects>)




![png](output_33_1.png)


### Summary <a id="sum"></a>
So there you have it! Quick and easy visuals and how to import data from .xlsx or .csv files. Bon voyage!

Remember:


```python
#Import to Module
import pandas as pd
```


```python
#Load a spreadsheet as a DataFrame using Pandas
df = pd.read_excel(filename)  
#or  
df = pd.read_csv(filename)
```


```python
# Make sure that graphs show up in Jupyter Notebook:  
%matplotlib inline 

df[[x_col, y_col]].plot(kind='barh') #Create a bar chart!
```

### [Back to Top](#top)

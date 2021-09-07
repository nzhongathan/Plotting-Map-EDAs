# Plotting Map EDAs
Plotting graphs for EDAs are a common thing in machine learning and data science tasks and using world maps as EDAs takes this one step further. I will be using Geopandas in order to show how to plot maps from data, depicting the data in variations of colors, as well as showing what we can learn from these maps about the world. In here you will find:
- Detailed Explanations On How To Create Map Graphs
- Sample Code and Walkthroughs Using the World Happiness Data

![a](https://miro.medium.com/max/3720/1*HevTonUoRkTNolFPO2P8Kw.png)

## Importing Libraries and Preparing Datasets
First, let's import several libraries that will help us. Most importantly, we have to import the Geopandas library, which will help us create a pandas Dataframe from "map data". These include:
- NumPy
- Pandas
- Matplotlib/Seaborn
- Math
- Geopandas

We will also have to load in the data. I will be using the World Happiness Index Reports as my data, so let's load those in first. I will be using the data from 2015-2019.
![Capture (24)](https://user-images.githubusercontent.com/69808907/132382065-7e5b7350-99f8-4b03-8349-e40507831a64.PNG)

For the "map", we will have to import a shapefile ('.shp'). This can be downloaded from various web sources online. I found the world map shapefile from [here](https://hub.arcgis.com/). Just upload the zip file into the Kaggle input section, and then use the geopands read_file function to import the shp file, similar to how we did for the .csv files.

![Capture(24)](https://user-images.githubusercontent.com/69808907/132382213-818ffead-5eff-4419-98fa-10222052dbc5.PNG)

There's our map! But first of, we need to standardize a couple names across the two Dataframes. There are several discrepencies on how certain countries are named, such as the "Russian Federation" instead of "Russia", or "Trinidad and Tobago" versus "Trinidad & Tobago". Let's handle this problem first.

Also, to simplify the data a little, I will create a new Dataframe with only the country names and their happiness score, as we will be visualizing that first. I will also be renaming one of the columns to make it easier to call on later on.

![Capture(25)](https://user-images.githubusercontent.com/69808907/132382331-f988eaf0-91e3-46e9-ad84-2aa6f3fdd6d1.PNG)

Great! Now let's merge the map_df dataframe with the world happiness score dataframe.

![Capture(26)](https://user-images.githubusercontent.com/69808907/132382405-f71cbdb1-c351-4d39-b4c8-1341bf40ea77.PNG)

Woah. That's a lot of NaN values! Let's handle that quickly. As you can see, there are many cases where territories and colonies are listed on the world map, but don't have a happiness index as they fit in with other countries, such as the American Samoa. Luckily, the map_df gave a "Country Affilation", which helps us handle many of these missing values.

First, I want to create a dictionary, letting the key be the country name and the key values being the happiness scores. I will also be appending several extra countries to the dictionary, since their information were not included in the 2019 dataset and their data were taken from previous happiness reports. These countries include:
- Maldives (2019)
- Oman (2016)
- Sudan (2017)
- Djibouti (2014)
- Angola (2017)
- Belize (2017)

Finally, I will create a simple for loop, which checks if the score is NaN, and will replace it if the Country Affilation is within the dictionary.

![Capture(27)](https://user-images.githubusercontent.com/69808907/132382576-074fffdf-9280-4833-baed-d5f6c48e4f4f.PNG)

Looks like most of our NaN values have been taken care of! Of course there are still a good amount of countries who weren't included in the 2019 World Happiness Report, or previous reports, so they will remain as NaN in our dataset.

This is the full list of unincluded countries:
- Samoa
- Tonga
- Fiji
- Antigua and Barbuda
- Aruba
- Bahamas
- Barbados
- Cuba
- Dominica
- Grenada
- Guyana
- Saint Kitts and Nevis
- Saint Lucia
- Saint Vincent and the Grenadines
- Suriname
- Cabo Verde
- Guinea-Bissau
- Sao Tome and Principe
- Eswatini
- Seychelles
- Equatorial Guinea
- Kiribati
- Eritrea
- Andorra
- Liechtenstein
- Monaco
- San Marino
- Vatican City
- Timor-Leste
- Nauru
- Papua New Guinea
- Solomon Islands
- Tuvalu
- Vanuatu
- Brunei Darussalam
- North Korea
- Marshall Islands
- Micronesia
- Palau

## Plotting the World Map
Now for the fun part ... the graphing. First let us define a couple variables that will be helpful later on. Our "variable" variable will be the data we want to represent in the world map, using different colors, and the vmin and vmax variables will represent the maximum and minimum values represented in our "variable" data.

Next, we will define our subplots, figure size, and plot our merged dataframe. We will define the "column" paramater to the "variable" variable, and you can adjust the edge color and line width to your liking. I chose to use the cmap "viridis" because it produces colors from yellow to purple, with yellow representing happier countries and purple representing less happy countries.

![Capture(28)](https://user-images.githubusercontent.com/69808907/132382967-65bbe7cb-c316-4afc-91b4-be33ac4b1997.PNG)

The map looks great already! But there are a couple more things we can add. First off, I will remove the axis and grids, as they don't provide any important information to this graph. Also I will add a quick title, as well as a scale on the side of the map. This scale will help viewers distinguish the color differences on the graph and help with understandability and readability.

![Capture(29)](https://user-images.githubusercontent.com/69808907/132383064-e26c807b-fb4a-446a-b0e8-4010a876b80b.PNG)

Beautiful! Our world map is now complete. Notice that countries where we have no data, such as Antarctica, North Korea, and Cuba, are depicted as white, as the NaN values are not taken into consideration in the cmap scale.

## What Does This Tell Us
Analyzing this map can show us multiple different things. First off, we can see how there is a lot of missing data specfically around the Oceania and Pacific Ocean region, which could be a focus for the World Happiness Index Report in future studies. Also we notice that the bulk of the happiest countries are located in the Northern Hemisphere, centered around North America and Northern Europe. Maybe colder weather and Northern environment can be an indication or hint as to how to improve happiness among countries as a whole. On the other hand, we notice the unhappiest countries are located in the Southern Hemisphere, centralized around Africa, which could be a focus for humanitarian efforts in the future.

There are also some anomolies that can noted here. First off, we notice that regions tend to share similar happiness scores, as bordering countries typically have very similar color schemes. Australia, though, is an exception, as it is by far the happiness country about of Oceania, Asia, and Africa. Likewise, we can notice heavy distinctions in the Middle East, with Saudi Arabia and Oman being a vastly lighter color than their neighbors, Yemen, Jordan, Iraq, etc.

All in all, though, this map can provide helpful insight on how geography and environment may affect happiness around the world, as we continue to study it.

## Some More Plots
Now that you know how to plot heatmaps using maps, I will be doing a couple other visualizations using the World Happiness Data. I will include my analysis of the graphs below it. (Disclaimer: I will not be inlcuding the added in data)

### Perception of Corruption
![Capture(30)](https://user-images.githubusercontent.com/69808907/132383209-d030d5c3-ca07-4137-9ae2-c8e82534cead.PNG)

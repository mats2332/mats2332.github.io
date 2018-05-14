---
layout: post
title: 2018-05-14-ArcGIS PythonAPI in Jupyter Notebook!
---

```python
#Mathew Suran
#DSSA-5103-91 Data Visualization
#DSSA-5104-91 Data Analysis
#Final Project-Analysis and Presentation
#05/12/18
```


```python
import os
import json
from IPython.display import display
import arcgis
from arcgis.gis import GIS
#from arcgis.mapping import WebMap
```


```python
gis = GIS("https://www.arcgis.com", "obx2332xdo", "8d%*FITr4jxIllqIY7!&#")
```

Creating new content
To create new items on your GIS, you use the add() method on ContentManager object. As earlier, you would not create this object, instead access it from the content property of your GIS object.

The add() method accepts a dictionary containing the properties of the item to be created. The optional data parameter accepts a string path to a file. You can use the optional metadata parameter to specify an XML file containing metadata information.

All content you add this way is added to the authenticated user's contents. Let us add a csv file and publish it as a feature layer.


```python
#file path or name
csv_file = 'NJBR_GIS2.csv'
#dictionary to specify properties
csv_properties={'title':'NJBR_Final',
                'description':'Beach Replenishment',
                'tags':'test'}
```


```python
#add content by specifying properties and data
NJBR_Final_csv = gis.content.add(item_properties=csv_properties, data=csv_file)
```

The add() method returns an object of type arcgis.gis.Item representing the added item.


```python
# Check the content
NJBR_Final_csv
```




<div class="item_container" style="height: auto; overflow: hidden; border: 1px solid #cfcfcf; border-radius: 2px; background: #f6fafa; line-height: 1.21429em; padding: 10px;">
                    <div class="item_left" style="width: 210px; float: left;">
                       <a href='https://obx2332xdo.maps.arcgis.com/home/item.html?id=5fda588d766e47cdb21ad92fee51cef1' target='_blank'>
                        <img src='http://static.arcgis.com/images/desktopapp.png' class="itemThumbnail">
                       </a>
                    </div>

                    <div class="item_right"     style="float: none; width: auto; overflow: hidden;">
                        <a href='https://obx2332xdo.maps.arcgis.com/home/item.html?id=5fda588d766e47cdb21ad92fee51cef1' target='_blank'><b>NJBR_Final</b>
                        </a>
                        <br/><img src='https://obx2332xdo.maps.arcgis.com/home/js/jsapi/esri/css/images/item_type_icons/layers16.png' style="vertical-align:middle;">CSV by obx2332xdo
                        <br/>Last Modified: May 14, 2018
                        <br/>0 comments, 0 views
                    </div>
                </div>
                




```python
# Create feature layer
NJBR_Final = NJBR_Final_csv.publish()
```


```python
# Check feature layer
NJBR_Final
```




<div class="item_container" style="height: auto; overflow: hidden; border: 1px solid #cfcfcf; border-radius: 2px; background: #f6fafa; line-height: 1.21429em; padding: 10px;">
                    <div class="item_left" style="width: 210px; float: left;">
                       <a href='https://obx2332xdo.maps.arcgis.com/home/item.html?id=53d6126082ef46f2a5314b845916d238' target='_blank'>
                        <img src='http://static.arcgis.com/images/desktopapp.png' class="itemThumbnail">
                       </a>
                    </div>

                    <div class="item_right"     style="float: none; width: auto; overflow: hidden;">
                        <a href='https://obx2332xdo.maps.arcgis.com/home/item.html?id=53d6126082ef46f2a5314b845916d238' target='_blank'><b>NJBR_Final</b>
                        </a>
                        <br/><img src='https://obx2332xdo.maps.arcgis.com/home/js/jsapi/esri/css/images/item_type_icons/featureshosted16.png' style="vertical-align:middle;">Feature Layer Collection by obx2332xdo
                        <br/>Last Modified: May 14, 2018
                        <br/>0 comments, 0 views
                    </div>
                </div>
                




```python
# create a new folder
new_folder_details = gis.content.create_folder("Final")
print(new_folder_details)
```

    {'username': 'obx2332xdo', 'id': '0949815124da4a8b825a45da332ae6b4', 'title': 'Final'}



```python
# move both the csv_item and csv_lyr items into this new folder
NJBR_Final_csv.move("Final")  # Here you could either pass name of the folder or the dictionary
                                   # returned from create_folder() or folders property on a User object

NJBR_Final.move("Final")
```




    {'folder': '0949815124da4a8b825a45da332ae6b4',
     'itemId': '53d6126082ef46f2a5314b845916d238',
     'owner': 'obx2332xdo',
     'success': True}




```python
# Return details of folder
print(NJBR_Final.ownerFolder)
```

    0949815124da4a8b825a45da332ae6b4



```python
# Create the map and specify extent
map2 = gis.map("New Jersey")
#map2.basemap = 'topo'
```


```python
#query the layers in the item
NJBR_Final.layers
```




    [<FeatureLayer url:"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0">]




```python
# Print the field names.
for field in NJBR_Final.layers[0].properties['fields']:
    print(field['name'])
```

    MUN
    Year
    Latitude
    Longitude
    Total_CY
    Costin2016
    FID



```python
# Use the above info to add layer to map
# Specify the renderer
map2.add_layer({"type":"FeatureLayer",
                "url":"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0",
                "renderer":"HeatmapRenderer",
                "field_name":"Total_CY"               
               })
map2
```




```python
## Optional Step is to save it to a Web Map to be saved and used in other applications
```


```python
webmap_properties = {'title':'Heatmap of Beach Replenishments Total Volumne (cu yd)',
                    'snippet': 'Jupyter notebook widget saved as a web map',
                    'tags':['automation', 'python']}

webmap_item = map2.save(webmap_properties, thumbnail='./webmap_thumbnail.png', folder='Final')
webmap_item
```

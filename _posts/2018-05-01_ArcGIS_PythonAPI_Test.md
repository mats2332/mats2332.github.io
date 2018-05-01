---
layout: post
title: ArcGIS Python Api
---

```python
from IPython.display import display
from arcgis.gis import GIS
import os
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
csv_properties={'title':'Beach_Replenishment_Final',
                'description':'This is a test',
                'tags':'test'}
#add content by specifying properties and data
NJBR_csv_item = gis.content.add(item_properties=csv_properties, data=csv_file)
```

The add() method returns an object of type arcgis.gis.Item representing the added item.


```python
NJBR_csv_item
```


```python
NJBR_Feature_lyr = NJBR_csv_item.publish()
```


```python
NJBR_Feature_lyr
```


```python
# create a new folder called 'Rainfall Data'
#new_folder_details = gis.content.create_folder("Final Project")
#print(new_folder_details)
```


```python
# move both the csv_item and csv_lyr items into this new folder
NJBR_csv_item.move("Final Project")  # Here you could either pass name of the folder or the dictionary
                                   # returned from create_folder() or folders property on a User object

NJBR_Feature_lyr.move("Final Project")
```


```python
print(NJBR_Feature_lyr.ownerFolder)
```


```python
map2 = gis.map("New Jersey")
#map2.basemap = 'topo'
map2
```


```python
# Use the first layer available on the service.
#NJBR_Feature_lyr = NJBR_Feature_lyr.layers[0]
```


```python
# Print the layer's url and field names.
print(NJBR_Feature_lyr.url)
for field in NJBR_Feature_lyr.properties['fields']:
    print(field['name'])
```


```python
map2.add_layer({"type":"FeatureLayer",
                "url":"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/Beach_Replenishment_Final/FeatureServer/0",
                "renderer":"HeatmapRenderer",
                "field_name":"Total_CY"               
               })
```


```python
map2.add_layer({"type":"FeatureLayer",
                "url":"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/Beach_Replenishment_Final/FeatureServer/0",
                "renderer":"ClassedSizeRenderer",
                "field_name":"Total_CY",
                "opacity":0.75
               })
```


```python
flayer_search_result = gis.content.search("owner:obx2332xdo","Feature Layer", outside_org=True)
flayer_search_result
```


```python
NJBR_item = flayer_search_result[4]
map2.add_layer(NJBR_item)
print(NJBR_item.url)
```


```python
map2.add_layer(NJBR_item, {"type":"FeatureLayer",
                            "renderer":"ClassedSizeRenderer",
                            "field_name":"Total_CY"
                                  })
```


```python
map2.add_layer(NJBR_item, {"type":"FeatureLayer",                            
                            "renderer":"HeatmapRenderer",
                            "field_name":"Total_CY"
                                  })
```


```python
# List current layers on Map
map2.layers
```


```python
# Remove specified layers
map2.remove_layers(layers=[usa_freeways])
```


```python
# Remove all layers
map2.remove_layers(all)
```


```python
# Save the webmap
webmap_properties = {'title':'USA time zones and capitols',
                    'snippet': 'Jupyter notebook widget saved as a web map',
                    'tags':['automation', 'python']}

webmap_item = usa_map.save(webmap_properties, thumbnail='./webmap_thumbnail.png', folder='webmaps')
webmap_item
```


```python
#from arcgis.features import summarize_data
#specify field and statisticType [‘Count’, ‘Sum’, ‘Mean’, ‘Min’, ‘Max’, ‘Range’, ‘Stddev’, ‘Var’]
#sum_fields = ['Volume__CY_ Sum']
#(input_layer, fields: str = None, summary_fields: str = None, output_name: str = None, gis=None)
#eq_summary = summarize_data.aggregate_points(NJData_Feature_lyr,                                            
#                                            summary_fields=sum_fields)
```

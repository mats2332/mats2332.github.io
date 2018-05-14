---
layout: post
title: 2018-05-14-ArcGIS PythonAPI in Jupyter Notebook!
---

<script src="https://unpkg.com/jupyter-js-widgets@~2.1.5/dist/embed.js"></script>
<script type="application/vnd.jupyter.widget-state+json">
{
    "version_major": 1,
    "version_minor": 0,
    "state": {
        "54ef187f1f8c4a22a139bfd154c93433": {
            "model_name": "LayoutModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "~2.1.4",
            "state": {
                "_model_module_version": "~2.1.4",
                "_view_module_version": "~2.1.4"
            }
        },
        "c8d04ed6f4f346518dbc457b5ca04f68": {
            "model_name": "DOMWidgetModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "*",
            "state": {
                "_addlayer": "{\"type\": \"FeatureLayer\", \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0\", \"renderer\": \"HeatmapRenderer\", \"field_name\": \"Total_CY\"}",
                "_arcgis_url": "https://obx2332xdo.maps.arcgis.com/sharing/rest/content/items",
                "_basemap": "topo",
                "_extent": "{\"xmin\": -75.78856499999995, \"ymin\": 38.55334835300005, \"xmax\": -73.66856499999994, \"ymax\": 40.67334835300005}",
                "_gallerybasemaps": [],
                "_gbasemaps_def": [],
                "_js_basemap": "[{\"url\":\"http://services.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer\",\"title\":\"World Topographic Map\"}]",
                "_js_interactive_drawn_graphic": "",
                "_js_layer_list": "[{\"id\":\"graphicsLayer3\",\"normalization\":true,\"refreshInterval\":0,\"url\":\"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0\",\"renderer\":{\"type\":\"heatmap\",\"blurRadius\":10,\"colorStops\":[{\"ratio\":0,\"color\":[255,140,0,0]},{\"ratio\":0.75,\"color\":[255,140,0,255]},{\"ratio\":0.9,\"color\":[255,0,0,255]}],\"maxPixelIntensity\":100,\"minPixelIntensity\":0,\"field\":null},\"rendererType\":\"esri.renderer.HeatmapRenderer\"},{\"id\":\"graphicsLayer5\",\"normalization\":true,\"refreshInterval\":0,\"url\":\"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0\",\"renderer\":{\"type\":\"heatmap\",\"blurRadius\":10,\"colorStops\":[{\"ratio\":0,\"color\":[255,140,0,0]},{\"ratio\":0.75,\"color\":[255,140,0,255]},{\"ratio\":0.9,\"color\":[255,0,0,255]}],\"maxPixelIntensity\":100,\"minPixelIntensity\":0,\"field\":null},\"rendererType\":\"esri.renderer.HeatmapRenderer\"}]",
                "_js_renderer": "",
                "_jsextent": "",
                "_layerId_to_remove": "",
                "_model_name": "DOMWidgetModel",
                "_swipe_div": "swipeDiv01KR2S",
                "_token_info": "{\"server\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/\", \"tokenurl\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/generateToken\", \"username\": \"obx2332xdo\", \"password\": \"8d%*FITr4jxIllqIY7!&#\"}",
                "_view_module": "mapview",
                "_view_name": "MapView",
                "basemaps": [
                    "dark-gray",
                    "dark-gray-vector",
                    "gray",
                    "gray-vector",
                    "hybrid",
                    "national-geographic",
                    "oceans",
                    "osm",
                    "satellite",
                    "streets",
                    "streets-navigation-vector",
                    "streets-night-vector",
                    "streets-relief-vector",
                    "streets-vector",
                    "terrain",
                    "topo",
                    "topo-vector"
                ],
                "center": [
                    0,
                    0
                ],
                "end_time": "",
                "id": "",
                "layout": "IPY_MODEL_54ef187f1f8c4a22a139bfd154c93433",
                "mode": "navigate",
                "start_time": "",
                "width": "100%",
                "zoom": 2
            }
        },
        "ad4e0ff89e7141f893534215dfa0c28b": {
            "model_name": "LayoutModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "~2.1.4",
            "state": {
                "_model_module_version": "~2.1.4",
                "_view_module_version": "~2.1.4"
            }
        },
        "ef73b04b7b564e0d9a28be4b6cd89da0": {
            "model_name": "DOMWidgetModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "*",
            "state": {
                "_addlayer": "{\"type\": \"FeatureLayer\", \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0\", \"renderer\": \"HeatmapRenderer\", \"field_name\": \"Costin2016\"}",
                "_arcgis_url": "https://obx2332xdo.maps.arcgis.com/sharing/rest/content/items",
                "_basemap": "topo",
                "_extent": "{\"xmin\": -75.78856499999995, \"ymin\": 38.55334835300005, \"xmax\": -73.66856499999994, \"ymax\": 40.67334835300005}",
                "_gallerybasemaps": [],
                "_gbasemaps_def": [],
                "_js_basemap": "[{\"url\":\"http://services.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer\",\"title\":\"World Topographic Map\"}]",
                "_js_interactive_drawn_graphic": "",
                "_js_layer_list": "[{\"id\":\"graphicsLayer4\",\"normalization\":true,\"refreshInterval\":0,\"url\":\"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0\",\"renderer\":{\"type\":\"heatmap\",\"blurRadius\":10,\"colorStops\":[{\"ratio\":0,\"color\":[255,140,0,0]},{\"ratio\":0.75,\"color\":[255,140,0,255]},{\"ratio\":0.9,\"color\":[255,0,0,255]}],\"maxPixelIntensity\":100,\"minPixelIntensity\":0,\"field\":null},\"rendererType\":\"esri.renderer.HeatmapRenderer\"}]",
                "_js_renderer": "",
                "_jsextent": "",
                "_layerId_to_remove": "",
                "_model_name": "DOMWidgetModel",
                "_swipe_div": "swipeDivGTIXCR",
                "_token_info": "{\"server\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/\", \"tokenurl\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/generateToken\", \"username\": \"obx2332xdo\", \"password\": \"8d%*FITr4jxIllqIY7!&#\"}",
                "_view_module": "mapview",
                "_view_name": "MapView",
                "basemaps": [
                    "dark-gray",
                    "dark-gray-vector",
                    "gray",
                    "gray-vector",
                    "hybrid",
                    "national-geographic",
                    "oceans",
                    "osm",
                    "satellite",
                    "streets",
                    "streets-navigation-vector",
                    "streets-night-vector",
                    "streets-relief-vector",
                    "streets-vector",
                    "terrain",
                    "topo",
                    "topo-vector"
                ],
                "center": [
                    0,
                    0
                ],
                "end_time": "",
                "id": "",
                "layout": "IPY_MODEL_ad4e0ff89e7141f893534215dfa0c28b",
                "mode": "navigate",
                "start_time": "",
                "width": "100%",
                "zoom": 2
            }
        },
        "dac3adab6a724e20ad600bc031da4bc1": {
            "model_name": "LayoutModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "~2.1.4",
            "state": {
                "_model_module_version": "~2.1.4",
                "_view_module_version": "~2.1.4"
            }
        },
        "67b3562981314ec4a2d5e6bf0bf0293f": {
            "model_name": "DOMWidgetModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "*",
            "state": {
                "_addlayer": "{\"type\": \"FeatureLayer\", \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0\", \"renderer\": \"ClassedSizeRenderer\", \"field_name\": \"Year\"}",
                "_arcgis_url": "https://obx2332xdo.maps.arcgis.com/sharing/rest/content/items",
                "_basemap": "topo",
                "_extent": "{\"xmin\": -75.78856499999995, \"ymin\": 38.55334835300005, \"xmax\": -73.66856499999994, \"ymax\": 40.67334835300005}",
                "_gallerybasemaps": [],
                "_gbasemaps_def": [],
                "_js_basemap": "[{\"url\":\"http://services.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer\",\"title\":\"World Topographic Map\"}]",
                "_js_interactive_drawn_graphic": "",
                "_js_layer_list": "[{\"id\":\"graphicsLayer10\",\"normalization\":true,\"refreshInterval\":0,\"url\":\"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0\",\"renderer\":{\"type\":\"heatmap\",\"blurRadius\":10,\"colorStops\":[{\"ratio\":0,\"color\":[255,140,0,0]},{\"ratio\":0.75,\"color\":[255,140,0,255]},{\"ratio\":0.9,\"color\":[255,0,0,255]}],\"maxPixelIntensity\":100,\"minPixelIntensity\":0,\"field\":null},\"rendererType\":\"esri.renderer.HeatmapRenderer\"},{\"id\":\"graphicsLayer12\",\"normalization\":true,\"refreshInterval\":0,\"url\":\"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0\",\"renderer\":{\"type\":\"simple\",\"symbol\":{\"angle\":0,\"xoffset\":0,\"yoffset\":0,\"type\":\"esriPMS\",\"url\":\"RedSphere.png\",\"imageData\":\"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\",\"contentType\":\"image/png\",\"width\":15,\"height\":15}},\"rendererType\":\"esri.renderer.SimpleRenderer\"},{\"id\":\"graphicsLayer14\",\"normalization\":true,\"refreshInterval\":0,\"url\":\"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0\",\"renderer\":{\"type\":\"simple\",\"symbol\":{\"angle\":0,\"xoffset\":0,\"yoffset\":0,\"type\":\"esriPMS\",\"url\":\"RedSphere.png\",\"imageData\":\"iVBORw0KGgoAAAANSUhEUgAAAEAAAABACAYAAACqaXHeAAAABGdBTUEAALGPC/xhBQAAACBjSFJNAAB6JgAAgIQAAPoAAACA6AAAdTAAAOpgAAA6mAAAF3CculE8AAAACXBIWXMAAA7DAAAOwwHHb6hkAAAAGXRFWHRTb2Z0d2FyZQBQYWludC5ORVQgdjMuNS4xTuc4+QAAB3VJREFUeF7tmPlTlEcexnve94U5mANQbgQSbgiHXHINlxpRIBpRI6wHorLERUmIisKCQWM8cqigESVQS1Kx1piNi4mW2YpbcZONrilE140RCTcy3DDAcL/zbJP8CYPDL+9Ufau7uqb7eZ7P+/a8PS8hwkcgIBAQCAgEBAICAYGAQEAgIBAQCAgEBAICAYGAQEAgIBAQCDx/AoowKXFMUhD3lQrioZaQRVRS+fxl51eBTZUTdZ41U1Rox13/0JF9csGJ05Qv4jSz/YPWohtvLmSKN5iTGGqTm1+rc6weICOBRbZs1UVnrv87T1PUeovxyNsUP9P6n5cpHtCxu24cbrmwKLdj+osWiqrVKhI0xzbmZ7m1SpJ+1pFpvE2DPvGTomOxAoNLLKGLscZYvB10cbYYjrJCb7A5mrxleOBqim+cWJRakZY0JfnD/LieI9V1MrKtwokbrAtU4Vm0A3TJnphJD4B+RxD0u0LA7w7FTE4oprOCMbklEGNrfdGf4IqnQTb4wc0MFTYibZqM7JgjO8ZdJkpMln/sKu16pHZGb7IfptIWg389DPp9kcChWODoMuDdBOhL1JgpisbUvghM7AqFbtNiaFP80RLnhbuBdqi0N+1dbUpWGde9gWpuhFi95yL7sS7BA93JAb+Fn8mh4QujgPeTgb9kAZf3Apd2A+fXQ38yHjOHozB1IAJjOSEY2RSIwVUv4dd4X9wJccGHNrJ7CYQ4GGjLeNNfM+dyvgpzQstKf3pbB2A6m97uBRE0/Ergcxr8hyqg7hrwn0vAtRIKIRX6Y2pMl0RhIj8co9nBGFrvh55l3ngU7YObng7IVnFvGS+BYUpmHziY/Ls2zgP9SX50by/G9N5w6I+ogYvpwK1SoOlHQNsGfWcd9Peqof88B/rTyzF9hAIopAByQzC0JQB9ST5oVnvhnt+LOGsprvUhxNIwa0aY7cGR6Cp7tr8+whkjawIxkRWC6YJI6N+lAKq3Qf/Tx+B77oGfaQc/8hB8w2Xwtw9Bf3kzZspXY/JIDEbfpAB2BKLvVV90Jvjgoac9vpRxE8kciTVCBMMkNirJ7k/tRHyjtxwjKV4Yp3t/6s+R4E+/DH3N6+BrS8E314Dvvg2+/Sb4hxfBf5sP/up2TF3ZhonK1zD6dhwGdwail26DzqgX8MRKiq9ZBpkSkmeYOyPM3m9Jjl+1Z9D8AgNtlAq6bZ70qsZi+q+bwV/7I/hbB8D/dAr8Axq89iz474p/G5++koHJy1sx/lkGdBc2YjA3HF0rHNHuboomuQj/5DgclIvOGCGCYRKFFuTMV7YUAD3VDQaLMfyqBcZORGPy01QKYSNm/rYV/Nd/Av9NHvgbueBrsjDzRQamKKDxT9Kgq1iLkbIUDOSHoiNcgnYHgnYZi+9ZExSbiSoMc2eE2flKcuJLa4KGRQz6/U0wlGaP0feiMH4uFpMXEjBVlYjp6lWY+SSZtim0kulYMiYuJEJXuhTDJ9UYPByOvoIwdCxfgE4bAo0Jh39xLAoVpMwIEQyTyFCQvGpLon9sJ0K3J4OBDDcMH1dj9FQsxkrjMPFRPCbOx2GyfLal9VEcxstioTulxjAFNfROJPqLl6Bnfyg6V7ugz5yBhuHwrZjBdiU5YJg7I8wOpifAKoVIW7uQ3rpOBH2b3ekVjYT2WCRG3o+mIGKgO0OrlIaebU/HYOQDNbQnojB4NJyGD0NPfjA0bwTRE6Q7hsUcWhkWN8yZqSQlWWGECAZLmJfJmbrvVSI8taK37xpbdB/wQW8xPee/8xIGjvlj8IQ/hk4G0JbWcX8MHPVDX4kveoq8ocn3xLM33NCZRcPHOGJYZIKfpQyq7JjHS6yJjcHujLHADgkpuC7h8F8zEVqXSNC2awE69lqhs8AamkO26HrbDt2H7dBVQov2NcW26CiwQtu+BWjdY4n2nZboTbfCmKcCnRyDO/YmyLPnDlHvjDH8G6zhS9/wlEnYR7X00fWrFYuWdVI0ZpuhcbcczW/R2qdAcz6t/bRov4mONeaaoYl+p22rHF0bVNAmKtBvweIXGxNcfFH8eNlC4m6wMWMusEnKpn5hyo48pj9gLe4SNG9QoGGLAk8z5XiaJUd99u8122/IpBA2K9BGg2vWWKAvRYVeLzEa7E1R422m2+MsSTem97nSYnfKyN6/mzATv7AUgqcMrUnmaFlLX3ysM0fj+t/b5lQLtK22QEfyAmiSLKFZpUJ7kBRPXKW4HqCYynWVHKSG2LkyZex1uO1mZM9lKem9Tx9jjY5iNEYo0bKMhn7ZAu0r6H5PpLXCAq0rKJClSjSGynE/QIkrQYqBPe6S2X+AJsY2Ped6iWZk6RlL0c2r5szofRsO9R5S1IfQLRCpQL1aifoYFerpsbkuTImaUJXuXIDiH6/Ys8vm3Mg8L2i20YqsO7fItKLcSXyn0kXccclVqv3MS6at9JU/Ox+ouns+SF6Z4cSupz7l8+z1ucs7LF1AQjOdxfGZzmx8Iu1TRcfnrioICAQEAgIBgYBAQCAgEBAICAQEAgIBgYBAQCAgEBAICAQEAv8H44b/6ZiGvGAAAAAASUVORK5CYII=\",\"contentType\":\"image/png\",\"width\":15,\"height\":15}},\"rendererType\":\"esri.renderer.SimpleRenderer\"}]",
                "_js_renderer": "",
                "_jsextent": "",
                "_layerId_to_remove": "",
                "_model_name": "DOMWidgetModel",
                "_swipe_div": "swipeDivEA90HW",
                "_token_info": "{\"server\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/\", \"tokenurl\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/generateToken\", \"username\": \"obx2332xdo\", \"password\": \"8d%*FITr4jxIllqIY7!&#\"}",
                "_view_module": "mapview",
                "_view_name": "MapView",
                "basemaps": [
                    "dark-gray",
                    "dark-gray-vector",
                    "gray",
                    "gray-vector",
                    "hybrid",
                    "national-geographic",
                    "oceans",
                    "osm",
                    "satellite",
                    "streets",
                    "streets-navigation-vector",
                    "streets-night-vector",
                    "streets-relief-vector",
                    "streets-vector",
                    "terrain",
                    "topo",
                    "topo-vector"
                ],
                "center": [
                    0,
                    0
                ],
                "end_time": "",
                "id": "",
                "layout": "IPY_MODEL_dac3adab6a724e20ad600bc031da4bc1",
                "mode": "navigate",
                "start_time": "",
                "width": "100%",
                "zoom": 2
            }
        },
        "0686ecb7f9684328934fca2800598877": {
            "model_name": "LayoutModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "~2.1.4",
            "state": {
                "_model_module_version": "~2.1.4",
                "_view_module_version": "~2.1.4"
            }
        },
        "96c351248eaa4bb697d7aeafc2b40864": {
            "model_name": "DOMWidgetModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "*",
            "state": {
                "_addlayer": "{\"type\": \"FeatureLayer\", \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0\", \"renderer\": \"ClassedSizeRenderer\", \"field_name\": \"Total_CY\"}",
                "_arcgis_url": "https://obx2332xdo.maps.arcgis.com/sharing/rest/content/items",
                "_basemap": "topo",
                "_extent": "{\"xmin\": -75.78856499999995, \"ymin\": 38.55334835300005, \"xmax\": -73.66856499999994, \"ymax\": 40.67334835300005}",
                "_gallerybasemaps": [],
                "_gbasemaps_def": [],
                "_js_basemap": "[{\"url\":\"http://services.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer\",\"title\":\"World Topographic Map\"}]",
                "_js_interactive_drawn_graphic": "",
                "_js_layer_list": "[{\"id\":\"graphicsLayer17\",\"normalization\":true,\"refreshInterval\":0,\"url\":\"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0\",\"renderer\":{\"type\":\"simple\",\"symbol\":{\"angle\":0,\"xoffset\":0,\"yoffset\":0,\"type\":\"esriPMS\",\"url\":\"RedSphere.png\",\"imageData\":\"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\",\"contentType\":\"image/png\",\"width\":15,\"height\":15}},\"rendererType\":\"esri.renderer.SimpleRenderer\"}]",
                "_js_renderer": "",
                "_jsextent": "",
                "_layerId_to_remove": "",
                "_model_name": "DOMWidgetModel",
                "_swipe_div": "swipeDivKZ5M1N",
                "_token_info": "{\"server\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/\", \"tokenurl\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/generateToken\", \"username\": \"obx2332xdo\", \"password\": \"8d%*FITr4jxIllqIY7!&#\"}",
                "_view_module": "mapview",
                "_view_name": "MapView",
                "basemaps": [
                    "dark-gray",
                    "dark-gray-vector",
                    "gray",
                    "gray-vector",
                    "hybrid",
                    "national-geographic",
                    "oceans",
                    "osm",
                    "satellite",
                    "streets",
                    "streets-navigation-vector",
                    "streets-night-vector",
                    "streets-relief-vector",
                    "streets-vector",
                    "terrain",
                    "topo",
                    "topo-vector"
                ],
                "center": [
                    0,
                    0
                ],
                "end_time": "",
                "id": "",
                "layout": "IPY_MODEL_0686ecb7f9684328934fca2800598877",
                "mode": "navigate",
                "start_time": "",
                "width": "100%",
                "zoom": 2
            }
        },
        "f1a50f16c0da4f8ba5b3c85d6b2f4779": {
            "model_name": "LayoutModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "~2.1.4",
            "state": {
                "_model_module_version": "~2.1.4",
                "_view_module_version": "~2.1.4"
            }
        },
        "8bc26b0586ec4c8cb6831dd7b22c71a9": {
            "model_name": "DOMWidgetModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "*",
            "state": {
                "_addlayer": "{\"type\": \"FeatureLayer\", \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0\", \"renderer\": \"HeatmapRenderer\", \"field_name\": \"Total_CY\"}",
                "_arcgis_url": "https://obx2332xdo.maps.arcgis.com/sharing/rest/content/items",
                "_basemap": "topo",
                "_extent": "{\"xmin\": -75.78856499999995, \"ymin\": 38.55334835300005, \"xmax\": -73.66856499999994, \"ymax\": 40.67334835300005}",
                "_gallerybasemaps": [],
                "_gbasemaps_def": [],
                "_js_basemap": "[{\"url\":\"http://services.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer\",\"title\":\"World Topographic Map\"}]",
                "_js_interactive_drawn_graphic": "",
                "_js_layer_list": "[{\"id\":\"graphicsLayer20\",\"normalization\":true,\"refreshInterval\":0,\"url\":\"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0\",\"renderer\":{\"type\":\"heatmap\",\"blurRadius\":10,\"colorStops\":[{\"ratio\":0,\"color\":[255,140,0,0]},{\"ratio\":0.75,\"color\":[255,140,0,255]},{\"ratio\":0.9,\"color\":[255,0,0,255]}],\"maxPixelIntensity\":100,\"minPixelIntensity\":0,\"field\":null},\"rendererType\":\"esri.renderer.HeatmapRenderer\"}]",
                "_js_renderer": "",
                "_jsextent": "{\"type\":\"extent\",\"xmin\":-8620824.9392949,\"ymin\":4688786.938329284,\"xmax\":-8016666.667728897,\"ymax\":4933385.428841836,\"spatialReference\":{\"wkid\":102100,\"latestWkid\":3857}}",
                "_layerId_to_remove": "",
                "_model_name": "DOMWidgetModel",
                "_swipe_div": "swipeDivKA3X5L",
                "_token_info": "{\"server\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/\", \"tokenurl\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/generateToken\", \"username\": \"obx2332xdo\", \"password\": \"8d%*FITr4jxIllqIY7!&#\"}",
                "_view_module": "mapview",
                "_view_name": "MapView",
                "basemaps": [
                    "dark-gray",
                    "dark-gray-vector",
                    "gray",
                    "gray-vector",
                    "hybrid",
                    "national-geographic",
                    "oceans",
                    "osm",
                    "satellite",
                    "streets",
                    "streets-navigation-vector",
                    "streets-night-vector",
                    "streets-relief-vector",
                    "streets-vector",
                    "terrain",
                    "topo",
                    "topo-vector"
                ],
                "center": [
                    0,
                    0
                ],
                "end_time": "",
                "id": "",
                "layout": "IPY_MODEL_f1a50f16c0da4f8ba5b3c85d6b2f4779",
                "mode": "navigate",
                "start_time": "",
                "width": "100%",
                "zoom": 2
            }
        },
        "b58714af7c2f44a28bdc07147ff21be8": {
            "model_name": "LayoutModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "~2.1.4",
            "state": {
                "_model_module_version": "~2.1.4",
                "_view_module_version": "~2.1.4"
            }
        },
        "f5cad5d34e5245bd97b921b3c171d25f": {
            "model_name": "DOMWidgetModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "*",
            "state": {
                "_addlayer": "{\"type\": \"FeatureLayer\", \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0?token=qU8aX7PmMHpPdnxoOBrWqWUpTKD5k4Su0VNkwSTet2Bo3G022zlHwEd_sieMF5atEKcL4XNCS0dbg6zj2ODX35G4KW3xVLCitgHTbt65Omc8wxWmtKVBswzRMbJ7ZDKL9tOVRpMcfFaBTrMy-2P4Wg..\", \"options\": \"{\\\"renderer\\\": \\\"HeatmapRenderer\\\", \\\"field_name\\\": \\\"Total_CY\\\"}\"}",
                "_arcgis_url": "https://obx2332xdo.maps.arcgis.com/sharing/rest/content/items",
                "_basemap": "topo",
                "_extent": "{\"xmin\": -75.78856499999995, \"ymin\": 38.55334835300005, \"xmax\": -73.66856499999994, \"ymax\": 40.67334835300005}",
                "_gallerybasemaps": [],
                "_gbasemaps_def": [],
                "_js_basemap": "[{\"url\":\"http://services.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer\",\"title\":\"World Topographic Map\"}]",
                "_js_interactive_drawn_graphic": "",
                "_js_layer_list": "[{\"id\": \"graphicsLayer48\", \"normalization\": true, \"refreshInterval\": 0, \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0?token=qU8aX7PmMHpPdnxoOBrWqWUpTKD5k4Su0VNkwSTet2Bo3G022zlHwEd_sieMF5atEKcL4XNCS0dbg6zj2ODX35G4KW3xVLCitgHTbt65Omc8wxWmtKVBswzRMbJ7ZDKL9tOVRpMcfFaBTrMy-2P4Wg..\", \"renderer\": {\"type\": \"simple\", \"symbol\": {\"angle\": 0, \"xoffset\": 0, \"yoffset\": 0, \"type\": \"esriPMS\", \"url\": \"RedSphere.png\", \"imageData\": \"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\", \"contentType\": \"image/png\", \"width\": 15, \"height\": 15}}, \"rendererType\": \"esri.renderer.SimpleRenderer\"}, {\"id\": \"graphicsLayer51\", \"normalization\": true, \"refreshInterval\": 0, \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0?token=qU8aX7PmMHpPdnxoOBrWqWUpTKD5k4Su0VNkwSTet2Bo3G022zlHwEd_sieMF5atEKcL4XNCS0dbg6zj2ODX35G4KW3xVLCitgHTbt65Omc8wxWmtKVBswzRMbJ7ZDKL9tOVRpMcfFaBTrMy-2P4Wg..\", \"renderer\": {\"type\": \"simple\", \"symbol\": {\"angle\": 0, \"xoffset\": 0, \"yoffset\": 0, \"type\": \"esriPMS\", \"url\": \"RedSphere.png\", \"imageData\": \"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\", \"contentType\": \"image/png\", \"width\": 15, \"height\": 15}}, \"rendererType\": \"esri.renderer.SimpleRenderer\"}, {\"id\": \"graphicsLayer53\", \"normalization\": true, \"refreshInterval\": 0, \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0?token=qU8aX7PmMHpPdnxoOBrWqWUpTKD5k4Su0VNkwSTet2Bo3G022zlHwEd_sieMF5atEKcL4XNCS0dbg6zj2ODX35G4KW3xVLCitgHTbt65Omc8wxWmtKVBswzRMbJ7ZDKL9tOVRpMcfFaBTrMy-2P4Wg..\", \"renderer\": {\"type\": \"heatmap\", \"blurRadius\": 10, \"colorStops\": [{\"ratio\": 0, \"color\": [255, 140, 0, 0]}, {\"ratio\": 0.75, \"color\": [255, 140, 0, 255]}, {\"ratio\": 0.9, \"color\": [255, 0, 0, 255]}], \"maxPixelIntensity\": 100, \"minPixelIntensity\": 0, \"field\": \"Total_CY\"}, \"rendererType\": \"esri.renderer.HeatmapRenderer\"}, {\"id\": \"graphicsLayer54\", \"normalization\": true, \"refreshInterval\": 0, \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0?token=qU8aX7PmMHpPdnxoOBrWqWUpTKD5k4Su0VNkwSTet2Bo3G022zlHwEd_sieMF5atEKcL4XNCS0dbg6zj2ODX35G4KW3xVLCitgHTbt65Omc8wxWmtKVBswzRMbJ7ZDKL9tOVRpMcfFaBTrMy-2P4Wg..\", \"renderer\": {\"type\": \"heatmap\", \"blurRadius\": 10, \"colorStops\": [{\"ratio\": 0, \"color\": [255, 140, 0, 0]}, {\"ratio\": 0.75, \"color\": [255, 140, 0, 255]}, {\"ratio\": 0.9, \"color\": [255, 0, 0, 255]}], \"maxPixelIntensity\": 100, \"minPixelIntensity\": 0, \"field\": \"Total_CY\"}, \"rendererType\": \"esri.renderer.HeatmapRenderer\"}, {\"id\": \"graphicsLayer55\", \"normalization\": true, \"refreshInterval\": 0, \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0?token=qU8aX7PmMHpPdnxoOBrWqWUpTKD5k4Su0VNkwSTet2Bo3G022zlHwEd_sieMF5atEKcL4XNCS0dbg6zj2ODX35G4KW3xVLCitgHTbt65Omc8wxWmtKVBswzRMbJ7ZDKL9tOVRpMcfFaBTrMy-2P4Wg..\", \"renderer\": {\"type\": \"simple\", \"symbol\": {\"angle\": 0, \"xoffset\": 0, \"yoffset\": 0, \"type\": \"esriPMS\", \"url\": \"RedSphere.png\", \"imageData\": \"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\", \"contentType\": \"image/png\", \"width\": 15, \"height\": 15}}, \"rendererType\": \"esri.renderer.SimpleRenderer\"}, {\"id\": \"graphicsLayer56\", \"normalization\": true, \"refreshInterval\": 0, \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0?token=qU8aX7PmMHpPdnxoOBrWqWUpTKD5k4Su0VNkwSTet2Bo3G022zlHwEd_sieMF5atEKcL4XNCS0dbg6zj2ODX35G4KW3xVLCitgHTbt65Omc8wxWmtKVBswzRMbJ7ZDKL9tOVRpMcfFaBTrMy-2P4Wg..\", \"renderer\": {\"type\": \"simple\", \"symbol\": {\"angle\": 0, \"xoffset\": 0, \"yoffset\": 0, \"type\": \"esriPMS\", \"url\": \"RedSphere.png\", \"imageData\": \"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\", \"contentType\": \"image/png\", \"width\": 15, \"height\": 15}}, \"rendererType\": \"esri.renderer.SimpleRenderer\"}, {\"id\": \"graphicsLayer58\", \"normalization\": true, \"refreshInterval\": 0, \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0?token=qU8aX7PmMHpPdnxoOBrWqWUpTKD5k4Su0VNkwSTet2Bo3G022zlHwEd_sieMF5atEKcL4XNCS0dbg6zj2ODX35G4KW3xVLCitgHTbt65Omc8wxWmtKVBswzRMbJ7ZDKL9tOVRpMcfFaBTrMy-2P4Wg..\", \"renderer\": {\"type\": \"heatmap\", \"blurRadius\": 10, \"colorStops\": [{\"ratio\": 0, \"color\": [255, 140, 0, 0]}, {\"ratio\": 0.75, \"color\": [255, 140, 0, 255]}, {\"ratio\": 0.9, \"color\": [255, 0, 0, 255]}], \"maxPixelIntensity\": 100, \"minPixelIntensity\": 0, \"field\": \"Total_CY\"}, \"rendererType\": \"esri.renderer.HeatmapRenderer\"}, {\"id\": \"graphicsLayer57\", \"normalization\": true, \"refreshInterval\": 0, \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0?token=qU8aX7PmMHpPdnxoOBrWqWUpTKD5k4Su0VNkwSTet2Bo3G022zlHwEd_sieMF5atEKcL4XNCS0dbg6zj2ODX35G4KW3xVLCitgHTbt65Omc8wxWmtKVBswzRMbJ7ZDKL9tOVRpMcfFaBTrMy-2P4Wg..\", \"renderer\": {\"type\": \"heatmap\", \"blurRadius\": 10, \"colorStops\": [{\"ratio\": 0, \"color\": [255, 140, 0, 0]}, {\"ratio\": 0.75, \"color\": [255, 140, 0, 255]}, {\"ratio\": 0.9, \"color\": [255, 0, 0, 255]}], \"maxPixelIntensity\": 100, \"minPixelIntensity\": 0, \"field\": \"Total_CY\"}, \"rendererType\": \"esri.renderer.HeatmapRenderer\"}, {\"id\": \"graphicsLayer60\", \"normalization\": true, \"refreshInterval\": 0, \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0?token=qU8aX7PmMHpPdnxoOBrWqWUpTKD5k4Su0VNkwSTet2Bo3G022zlHwEd_sieMF5atEKcL4XNCS0dbg6zj2ODX35G4KW3xVLCitgHTbt65Omc8wxWmtKVBswzRMbJ7ZDKL9tOVRpMcfFaBTrMy-2P4Wg..\", \"renderer\": {\"type\": \"heatmap\", \"blurRadius\": 10, \"colorStops\": [{\"ratio\": 0, \"color\": [255, 140, 0, 0]}, {\"ratio\": 0.75, \"color\": [255, 140, 0, 255]}, {\"ratio\": 0.9, \"color\": [255, 0, 0, 255]}], \"maxPixelIntensity\": 100, \"minPixelIntensity\": 0, \"field\": \"Total_CY\"}, \"rendererType\": \"esri.renderer.HeatmapRenderer\"}, {\"id\": \"graphicsLayer63\", \"normalization\": true, \"refreshInterval\": 0, \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0?token=qU8aX7PmMHpPdnxoOBrWqWUpTKD5k4Su0VNkwSTet2Bo3G022zlHwEd_sieMF5atEKcL4XNCS0dbg6zj2ODX35G4KW3xVLCitgHTbt65Omc8wxWmtKVBswzRMbJ7ZDKL9tOVRpMcfFaBTrMy-2P4Wg..\", \"renderer\": {\"type\": \"heatmap\", \"blurRadius\": 10, \"colorStops\": [{\"ratio\": 0, \"color\": [255, 140, 0, 0]}, {\"ratio\": 0.75, \"color\": [255, 140, 0, 255]}, {\"ratio\": 0.9, \"color\": [255, 0, 0, 255]}], \"maxPixelIntensity\": 100, \"minPixelIntensity\": 0, \"field\": \"Total_CY\"}, \"rendererType\": \"esri.renderer.HeatmapRenderer\"}]",
                "_js_renderer": "",
                "_jsextent": "{\"type\":\"extent\",\"xmin\":-8918572.655915843,\"ymin\":4575089.392038,\"xmax\":-7710256.112784098,\"ymax\":5064286.373062997,\"spatialReference\":{\"wkid\":102100,\"latestWkid\":3857}}",
                "_layerId_to_remove": "graphicsLayer46",
                "_model_name": "DOMWidgetModel",
                "_swipe_div": "swipeDivAFA4U5",
                "_token_info": "{\"server\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/\", \"tokenurl\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/generateToken\", \"username\": \"obx2332xdo\", \"password\": \"8d%*FITr4jxIllqIY7!&#\"}",
                "_view_module": "mapview",
                "_view_name": "MapView",
                "basemaps": [
                    "dark-gray",
                    "dark-gray-vector",
                    "gray",
                    "gray-vector",
                    "hybrid",
                    "national-geographic",
                    "oceans",
                    "osm",
                    "satellite",
                    "streets",
                    "streets-navigation-vector",
                    "streets-night-vector",
                    "streets-relief-vector",
                    "streets-vector",
                    "terrain",
                    "topo",
                    "topo-vector"
                ],
                "center": [
                    0,
                    0
                ],
                "end_time": "",
                "id": "",
                "layout": "IPY_MODEL_b58714af7c2f44a28bdc07147ff21be8",
                "mode": "navigate",
                "start_time": "",
                "width": "100%",
                "zoom": 2
            }
        },
        "ce8ef0259fe44d6c8c00216cf01d5eec": {
            "model_name": "LayoutModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "~2.1.4",
            "state": {
                "_model_module_version": "~2.1.4",
                "_view_module_version": "~2.1.4"
            }
        },
        "ce00a8d2abdf4b11901fbb4f8d9ad142": {
            "model_name": "DOMWidgetModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "*",
            "state": {
                "_addlayer": "{\"type\": \"FeatureLayer\", \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0?token=qU8aX7PmMHpPdnxoOBrWqWUpTKD5k4Su0VNkwSTet2Bo3G022zlHwEd_sieMF5atEKcL4XNCS0dbg6zj2ODX35G4KW3xVLCitgHTbt65Omc8wxWmtKVBswzRMbJ7ZDKL9tOVRpMcfFaBTrMy-2P4Wg..\", \"options\": \"{\\\"renderer\\\": \\\"HeatmapRenderer\\\", \\\"field_name\\\": \\\"Total_CY\\\"}\"}",
                "_arcgis_url": "https://obx2332xdo.maps.arcgis.com/sharing/rest/content/items",
                "_basemap": "topo",
                "_extent": "{\"xmin\": -75.78856499999995, \"ymin\": 38.55334835300005, \"xmax\": -73.66856499999994, \"ymax\": 40.67334835300005}",
                "_gallerybasemaps": [],
                "_gbasemaps_def": [],
                "_js_basemap": "[{\"url\":\"http://services.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer\",\"title\":\"World Topographic Map\"}]",
                "_js_interactive_drawn_graphic": "",
                "_js_layer_list": "[{\"id\":\"graphicsLayer67\",\"normalization\":true,\"refreshInterval\":0,\"url\":\"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJBR_Final/FeatureServer/0?token=qU8aX7PmMHpPdnxoOBrWqWUpTKD5k4Su0VNkwSTet2Bo3G022zlHwEd_sieMF5atEKcL4XNCS0dbg6zj2ODX35G4KW3xVLCitgHTbt65Omc8wxWmtKVBswzRMbJ7ZDKL9tOVRpMcfFaBTrMy-2P4Wg..\",\"renderer\":{\"type\":\"heatmap\",\"blurRadius\":10,\"colorStops\":[{\"ratio\":0,\"color\":[255,140,0,0]},{\"ratio\":0.75,\"color\":[255,140,0,255]},{\"ratio\":0.9,\"color\":[255,0,0,255]}],\"maxPixelIntensity\":100,\"minPixelIntensity\":0,\"field\":\"Total_CY\"},\"rendererType\":\"esri.renderer.HeatmapRenderer\"}]",
                "_js_renderer": "",
                "_jsextent": "",
                "_layerId_to_remove": "",
                "_model_name": "DOMWidgetModel",
                "_swipe_div": "swipeDivJD2LWI",
                "_token_info": "{\"server\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/\", \"tokenurl\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/generateToken\", \"username\": \"obx2332xdo\", \"password\": \"8d%*FITr4jxIllqIY7!&#\"}",
                "_view_module": "mapview",
                "_view_name": "MapView",
                "basemaps": [
                    "dark-gray",
                    "dark-gray-vector",
                    "gray",
                    "gray-vector",
                    "hybrid",
                    "national-geographic",
                    "oceans",
                    "osm",
                    "satellite",
                    "streets",
                    "streets-navigation-vector",
                    "streets-night-vector",
                    "streets-relief-vector",
                    "streets-vector",
                    "terrain",
                    "topo",
                    "topo-vector"
                ],
                "center": [
                    0,
                    0
                ],
                "end_time": "",
                "id": "",
                "layout": "IPY_MODEL_ce8ef0259fe44d6c8c00216cf01d5eec",
                "mode": "navigate",
                "start_time": "",
                "width": "100%",
                "zoom": 2
            }
        },
        "65da3c8e18744d42be8f33d360ec7543": {
            "model_name": "LayoutModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "~2.1.4",
            "state": {
                "_model_module_version": "~2.1.4",
                "_view_module_version": "~2.1.4"
            }
        },
        "842a1532a4604c14a2ed474d376c5249": {
            "model_name": "DOMWidgetModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "*",
            "state": {
                "_addlayer": "{\"type\": \"FeatureLayer\", \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/Beach_Replenishment_Final/FeatureServer/0\", \"renderer\": \"HeatmapRenderer\", \"field_name\": \"Total_CY\"}",
                "_arcgis_url": "https://obx2332xdo.maps.arcgis.com/sharing/rest/content/items",
                "_basemap": "topo",
                "_extent": "{\"xmin\": -75.78856499999995, \"ymin\": 38.55334835300005, \"xmax\": -73.66856499999994, \"ymax\": 40.67334835300005}",
                "_gallerybasemaps": [],
                "_gbasemaps_def": [],
                "_js_basemap": "[{\"url\":\"http://services.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer\",\"title\":\"World Topographic Map\"}]",
                "_js_interactive_drawn_graphic": "",
                "_js_layer_list": "[{\"id\":\"graphicsLayer70\",\"normalization\":true,\"refreshInterval\":0,\"url\":\"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/Beach_Replenishment_Final/FeatureServer/0?token=qzYYNvgcRFjXr3zAN3hw8id7pZGoeX4h0GM_VhcOxPAmPm36pL6DHYZY6majj6mItw5GCrTRX5BPyWNeJddEoKgOvnhVvAT7GeX7GNZZOdGcMhlbMganujLIVCPAu7LjHBUzi7iPiGCyYORQ_6wsiA..\",\"renderer\":{\"type\":\"simple\",\"symbol\":{\"angle\":0,\"xoffset\":0,\"yoffset\":0,\"type\":\"esriPMS\",\"url\":\"RedSphere.png\",\"imageData\":\"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\",\"contentType\":\"image/png\",\"width\":15,\"height\":15}},\"rendererType\":\"esri.renderer.SimpleRenderer\"}]",
                "_js_renderer": "",
                "_jsextent": "{\"type\":\"extent\",\"xmin\":-8612263.99212696,\"ymin\":4699793.870402349,\"xmax\":-8008105.720560958,\"ymax\":4944392.360914901,\"spatialReference\":{\"wkid\":102100,\"latestWkid\":3857}}",
                "_layerId_to_remove": "",
                "_model_name": "DOMWidgetModel",
                "_swipe_div": "swipeDiv0A9OP4",
                "_token_info": "{\"server\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/\", \"tokenurl\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/generateToken\", \"username\": \"obx2332xdo\", \"password\": \"8d%*FITr4jxIllqIY7!&#\"}",
                "_view_module": "mapview",
                "_view_name": "MapView",
                "basemaps": [
                    "dark-gray",
                    "dark-gray-vector",
                    "gray",
                    "gray-vector",
                    "hybrid",
                    "national-geographic",
                    "oceans",
                    "osm",
                    "satellite",
                    "streets",
                    "streets-navigation-vector",
                    "streets-night-vector",
                    "streets-relief-vector",
                    "streets-vector",
                    "terrain",
                    "topo",
                    "topo-vector"
                ],
                "center": [
                    0,
                    0
                ],
                "end_time": "",
                "id": "",
                "layout": "IPY_MODEL_65da3c8e18744d42be8f33d360ec7543",
                "mode": "navigate",
                "start_time": "",
                "width": "100%",
                "zoom": 2
            }
        },
        "9eb70108713c4ed091524dcd77845ddc": {
            "model_name": "LayoutModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "~2.1.4",
            "state": {
                "_model_module_version": "~2.1.4",
                "_view_module_version": "~2.1.4"
            }
        },
        "9aaf507cf4e3465baa3ccc72f2e1982c": {
            "model_name": "DOMWidgetModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "*",
            "state": {
                "_addlayer": "{\"type\": \"FeatureLayer\", \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/Beach_Replenishment_Final/FeatureServer/0\", \"renderer\": \"HeatmapRenderer\", \"field_name\": \"Total_CY\"}",
                "_arcgis_url": "https://obx2332xdo.maps.arcgis.com/sharing/rest/content/items",
                "_basemap": "topo",
                "_extent": "{\"xmin\": -75.78856499999995, \"ymin\": 38.55334835300005, \"xmax\": -73.66856499999994, \"ymax\": 40.67334835300005}",
                "_gallerybasemaps": [],
                "_gbasemaps_def": [],
                "_js_basemap": "[{\"url\":\"http://services.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer\",\"title\":\"World Topographic Map\"}]",
                "_js_interactive_drawn_graphic": "",
                "_js_layer_list": "",
                "_js_renderer": "",
                "_jsextent": "{\"type\":\"extent\",\"xmin\":-8613486.984579524,\"ymin\":4705297.336438881,\"xmax\":-8009328.71301352,\"ymax\":4949895.826951433,\"spatialReference\":{\"wkid\":102100,\"latestWkid\":3857}}",
                "_layerId_to_remove": "",
                "_model_name": "DOMWidgetModel",
                "_swipe_div": "swipeDiv2ZKPFA",
                "_token_info": "{\"server\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/\", \"tokenurl\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/generateToken\", \"username\": \"obx2332xdo\", \"password\": \"8d%*FITr4jxIllqIY7!&#\"}",
                "_view_module": "mapview",
                "_view_name": "MapView",
                "basemaps": [
                    "dark-gray",
                    "dark-gray-vector",
                    "gray",
                    "gray-vector",
                    "hybrid",
                    "national-geographic",
                    "oceans",
                    "osm",
                    "satellite",
                    "streets",
                    "streets-navigation-vector",
                    "streets-night-vector",
                    "streets-relief-vector",
                    "streets-vector",
                    "terrain",
                    "topo",
                    "topo-vector"
                ],
                "center": [
                    0,
                    0
                ],
                "end_time": "",
                "id": "",
                "layout": "IPY_MODEL_9eb70108713c4ed091524dcd77845ddc",
                "mode": "navigate",
                "start_time": "",
                "width": "100%",
                "zoom": 2
            }
        },
        "155fbc73e30b4b16bc79acbebdfa092e": {
            "model_name": "LayoutModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "~2.1.4",
            "state": {
                "_model_module_version": "~2.1.4",
                "_view_module_version": "~2.1.4"
            }
        },
        "e02e850cfc6c47bdbdb04c21f991ddc9": {
            "model_name": "DOMWidgetModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "*",
            "state": {
                "_addlayer": "{\"type\": \"FeatureLayer\", \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/Beach_Replenishment_Final/FeatureServer/0\", \"renderer\": \"HeatmapRenderer\", \"field_name\": \"Total_CY\"}",
                "_arcgis_url": "https://obx2332xdo.maps.arcgis.com/sharing/rest/content/items",
                "_basemap": "topo",
                "_extent": "{\"xmin\": -75.78856499999995, \"ymin\": 38.55334835300005, \"xmax\": -73.66856499999994, \"ymax\": 40.67334835300005}",
                "_gallerybasemaps": [],
                "_gbasemaps_def": [],
                "_js_basemap": "[{\"url\":\"http://services.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer\",\"title\":\"World Topographic Map\"}]",
                "_js_interactive_drawn_graphic": "",
                "_js_layer_list": "",
                "_js_renderer": "",
                "_jsextent": "",
                "_layerId_to_remove": "",
                "_model_name": "DOMWidgetModel",
                "_swipe_div": "swipeDivMVWQEA",
                "_token_info": "{\"server\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/\", \"tokenurl\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/generateToken\", \"username\": \"obx2332xdo\", \"password\": \"8d%*FITr4jxIllqIY7!&#\"}",
                "_view_module": "mapview",
                "_view_name": "MapView",
                "basemaps": [
                    "dark-gray",
                    "dark-gray-vector",
                    "gray",
                    "gray-vector",
                    "hybrid",
                    "national-geographic",
                    "oceans",
                    "osm",
                    "satellite",
                    "streets",
                    "streets-navigation-vector",
                    "streets-night-vector",
                    "streets-relief-vector",
                    "streets-vector",
                    "terrain",
                    "topo",
                    "topo-vector"
                ],
                "center": [
                    0,
                    0
                ],
                "end_time": "",
                "id": "",
                "layout": "IPY_MODEL_155fbc73e30b4b16bc79acbebdfa092e",
                "mode": "navigate",
                "start_time": "",
                "width": "100%",
                "zoom": 2
            }
        },
        "a5303fb16e3a48f28cb13a6abe19058c": {
            "model_name": "LayoutModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "~2.1.4",
            "state": {
                "_model_module_version": "~2.1.4",
                "_view_module_version": "~2.1.4"
            }
        },
        "9ba3b7087088400f897fd9673a74ea3f": {
            "model_name": "DOMWidgetModel",
            "model_module": "jupyter-js-widgets",
            "model_module_version": "*",
            "state": {
                "_addlayer": "{\"type\": \"FeatureLayer\", \"url\": \"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJData2/FeatureServer/0\", \"renderer\": \"HeatmapRenderer\", \"field_name\": \"Volume__CY_\"}",
                "_arcgis_url": "https://obx2332xdo.maps.arcgis.com/sharing/rest/content/items",
                "_basemap": "topo",
                "_extent": "{\"xmin\": -75.78856499999995, \"ymin\": 38.55334835300005, \"xmax\": -73.66856499999994, \"ymax\": 40.67334835300005}",
                "_gallerybasemaps": [],
                "_gbasemaps_def": [],
                "_js_basemap": "[{\"url\":\"http://services.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer\",\"title\":\"World Topographic Map\"}]",
                "_js_interactive_drawn_graphic": "",
                "_js_layer_list": "[{\"id\":\"graphicsLayer96\",\"normalization\":true,\"refreshInterval\":0,\"url\":\"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJData2/FeatureServer/0\",\"renderer\":{\"type\":\"heatmap\",\"blurRadius\":10,\"colorStops\":[{\"ratio\":0,\"color\":[255,140,0,0]},{\"ratio\":0.75,\"color\":[255,140,0,255]},{\"ratio\":0.9,\"color\":[255,0,0,255]}],\"maxPixelIntensity\":100,\"minPixelIntensity\":0,\"field\":null},\"rendererType\":\"esri.renderer.HeatmapRenderer\"},{\"id\":\"graphicsLayer98\",\"normalization\":true,\"refreshInterval\":0,\"url\":\"https://services.arcgis.com/jAkM70Lb48wAd2b1/arcgis/rest/services/NJData2/FeatureServer/0\",\"renderer\":{\"type\":\"heatmap\",\"blurRadius\":10,\"colorStops\":[{\"ratio\":0,\"color\":[255,140,0,0]},{\"ratio\":0.75,\"color\":[255,140,0,255]},{\"ratio\":0.9,\"color\":[255,0,0,255]}],\"maxPixelIntensity\":100,\"minPixelIntensity\":0,\"field\":null},\"rendererType\":\"esri.renderer.HeatmapRenderer\"}]",
                "_js_renderer": "",
                "_jsextent": "{\"type\":\"extent\",\"xmin\":-8592696.112885958,\"ymin\":4697959.3817235045,\"xmax\":-7988537.841319954,\"ymax\":4942557.872236056,\"spatialReference\":{\"wkid\":102100,\"latestWkid\":3857},\"cache\":{\"_parts\":[{\"extent\":{\"type\":\"extent\",\"xmin\":-8592696.112885958,\"ymin\":4697959.3817235045,\"xmax\":-7988537.841319954,\"ymax\":4942557.872236056,\"spatialReference\":{\"wkid\":102100,\"latestWkid\":3857}},\"frameIds\":[0]}]}}",
                "_layerId_to_remove": "",
                "_model_name": "DOMWidgetModel",
                "_swipe_div": "swipeDiv7YUQWU",
                "_token_info": "{\"server\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/\", \"tokenurl\": \"https://obx2332xdo.maps.arcgis.com/sharing/rest/generateToken\", \"username\": \"obx2332xdo\", \"password\": \"8d%*FITr4jxIllqIY7!&#\"}",
                "_view_module": "mapview",
                "_view_name": "MapView",
                "basemaps": [
                    "dark-gray",
                    "dark-gray-vector",
                    "gray",
                    "gray-vector",
                    "hybrid",
                    "national-geographic",
                    "oceans",
                    "osm",
                    "satellite",
                    "streets",
                    "streets-navigation-vector",
                    "streets-night-vector",
                    "streets-relief-vector",
                    "streets-vector",
                    "terrain",
                    "topo",
                    "topo-vector"
                ],
                "center": [
                    0,
                    0
                ],
                "end_time": "",
                "id": "",
                "layout": "IPY_MODEL_a5303fb16e3a48f28cb13a6abe19058c",
                "mode": "navigate",
                "start_time": "",
                "width": "100%",
                "zoom": 2
            }
        }
    }
}
</script>
<script type="application/vnd.jupyter.widget-view+json">
{
    "model_id": "8bc26b0586ec4c8cb6831dd7b22c71a9"
}
</script>


```python
import os
import json
from IPython.display import display
import arcgis
from arcgis.gis import GIS
#from arcgis.mapping import WebMap
```


```python
gis = GIS("https://www.arcgis.com", "username", "password")
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

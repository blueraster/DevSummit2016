Building a Web App for Data Exploration with Smart Mapping
==========================================================

#### esri/styles
* Lots of colormaps or schemes
* Check out choropleth module
* Some color ramps are color blind safe

#### esri/plugins
* FeatureLayerStatistics, tons of good stuff
* Get many statistics about a certain field, this can be aware of your definition expressions
* getSampleFeatures
* getHistogram
* This can replace statistic definitions in Query Tasks

```javascript
featureLayer.addPlugin('esri/plugins/FeatureLayerStatistics')
```

#### esri/renderers
* smartMapping
* this can help get values to construct visualVariables
* smartMapping.createColorRenderer
  * returns a promise with a renderer so we can set ```layer.setRenderer(result.renderer)```

#### Other Modules
* esri/dijit/ColorInfoSlider

#### Other things to note
* smartMapping is a little expensive
* Sample Url: github.com/ekenes/esri-js-samples
  * smart-mapping

Questions

* How will it handle getting the correct color themes when we use the new Basemap class in 4.0?
* When will this functionality be available in 4.0?

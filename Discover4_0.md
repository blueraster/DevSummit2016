Discover 4.0
============

#### Overview
* Better design of API and Widgets
* Better WebMap integration
* New Portal API
* Working with the API
  * This section will cover many of the important changes and features
* esri/core
  * Accessor
    * base of most of the API
    * Consistent gets and sets throughout the API
    * Simple way to watch properties
    * Unified object constructor
    * autocast
    * Watching
      * No more property change events, just watchers
      * chain watching
    * createSubclass helper methods to create your own model
  * Promises everywhere, no more events
    * classes may be promises
    * ```view.then()``` replaces ```map.on('load', ...)```
  * Loadables
    * extension of promises
    * better scheduling of loading resources
    * views automatically load
    * maps and webmaps don't, but give the option to load them explicitly so you can only load what you need
  * Collections
    * like an array
    * in house methods of add/remove
    * arrayMethods plus some new ones like find and findIndex
    * emit change events for added/removed/moved items
    * autocasting support

#### Map and View Architecture
* 2D and 3D are isolated
* Views - MapView and SceneView
* Model - Map, WebMap, WebScene
* SceneViews should render WebScenes
* MapViews should render Maps
* You can easily create multiple views
* LayerViews API is limited but coming soon
* View.allLayerViews contains a list of all the layers

#### Basemap
* basemap layers are not part of the map.layers, but map.basemap
* can be set with string for esri's basemap or custom basemap instance
* contains 2 collections, baseLayers and referenceLayers

#### GroupLayer
* Group layers together
* listMode: hide-children or hidden, this hides them from TOC
* visibilityModes (exclusive, independent) are like radio button or checkbox functionality

#### Also Layers
* Also you can now mix image and graphics layers
* shorter names
* ArcGISElevationLayer
* SceneLayer

#### Animation
* ```view.goTo()```
* options will support duration and animation method like easing etc.
* view.goTo is a promise

```javascript
view.goTo(results.features, { duration: 300 })
view.goTo(layer, { duration: 300 });
view.goTo(someExtent, { duration: 300 });
view.goTo({ zoom: 5 }, { duration: 300 });
```

#### Environment
* 3D Feature Only
* Defines light characteristics
* starsEnabled
* lighting
  * ambientOcclusionEnabled
  * date
  * directShadowsEnabled

#### Portal API
* redesigned API
* much more functionality
* still very much in development
* Layer.fromPortalItem

#### WebMap and WebScene
* Full WebScene support
* WebMaps will not support all layers, only key layers, layers not supported will degrade to UnsupportedLayer
* Full webmap support by end of 2016
* WebMap and WebScene have similar properties to Maps but can have some extras
* WebScene had local and global viewing modes, local is better for smaller or underground viewing

#### UI and Widgets
* Popups have docking and custom actions support
* Easier to style widgets and vector tiles
* SASS available from bower installs
* ViewModels
  * business logic available for all widgets

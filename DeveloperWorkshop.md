# Developer Workshop

#### Quick Links
[JavaScript 4.0](#javascript-api-4.0)<br>
[Quartz Runtime](#quartz-runtime)<br>
[iOS Quartz](#ios-quartz)<br>
[Android Quartz](#android-quartz)<br>
[Java SDK](#java-sdk)<br>
[Qt/QML SDK](#qt/qml-sdk)<br>
[.Net SDK](#qt/.net-sdk)<br>

JavaScript API 4.0
------------------

#### New Features
* Portal API
* WebMap and WebScene
* Basemap
* GroupLayer
* Views

#### Portal Api
* Simplified API for accessing AGOL
* Handles auth and queries easily
* Load layers from portal api

```javascript
Layer.fromPortalItem().then((layer) => {
  map.addLayer(layer)
}).otherwise(error)
```
* This can bring in Popup configurations, renderers, and more.

#### WebMap and WebScene
* Support for all layers by end of 2016, layers not supported will be of type UnsupportedLayer
* Basemaps and Layers now universal between these two
* Each will have their own presentation items/style
* Can create them with a portalId
* Built on WebGL, so performance on mobile may not be there yet
* WebScenes have a slides API to easily thumbnails that act like the old bookmarks API

#### Basemaps
* Easier way to set
* Not part of map.layers anymore
* contains baseLayers and reference layers
* Easy to add third party services like stamen tiles as a basemap and not a different layer

#### GroupLayer
* Group layers together
* Structure your data visualization
* Has visibilityModes to define behavior/relationships for the group
* Supports list mode for the TOC
* Easier access to info for building custom components

```javascript
const groupLayer = new GroupLayer({
  title: '',
  visibilityMode: '',
  layers: [
    new TiledLayer(),
    ...layers
  ]
})
```

#### Views
* MapView and SceneViews separate business logic and drawing logic
* Easy to support multiple views with a single map instance
* Better accessor methods for layers and other elements

#### Animation
* Easy to add animations for zoom, camera, extent properties
* Simpler API across both 2D and 3D versions

#### UI
* API has attributes to simplify supporting responsive design

#### Widgets
* Much easier method for adding custom actions to out of the box Widgets
* Widget logic is now separate from the UI implementation so its easier to create custom widgets
* Really easy to override css or use their sass file to build your own

#### Coding Patterns
* ```esri/core/Accessor```
* ```esri/core/Promise```
* ```esri/core/Loadable```
* ```esri/core/Collection```
* Components are stateful, similar to dojo/Stateful
* Consistent patterns with getters, setters, and observers
* no more property change events, use ```watch()```

```javascript
map.watch('basemap.title', (value) => {});
map.watch('scale, extent', (value) => {});
```
* in 4.0, extent watchers will be called very often
* Single Object constructors, no more nested multiple constructors or multiple parameters
* Autocast to automatically convert input to the correct type if possible
* This can automatically convert JSON representation into the correct constructor
* new SimpleMarkerSymbol now only needs one constructor because of autocast, you can represent the whole symbol as one JSON object and it will create it for us vs creating line symbols and fill symbols and color objects.
* Accessor has helper methods for creating custom classes to model objects or other items

```javascript
Accessor.createSubclass({ ... })
```
* Everything async is promises now

#### JS Extras
* Graphics layers are in the same collection as other layers, so much easier to put other layers on top of graphics layers
* Better DOM structure, less DOM Vomit!!!!
* Better widgets
* Show stars and control lighting properties in the SceneView Environment
* Use a date in a sceneview to have accurate representations of sun, stars, and other environmental things

Quartz Runtime
--------------

#### Overview
* Major feature for this is a more consistent API for cross platform applications, not dumbed down but more consistent language across the APIs
* 3D, Local Analysis, Direct read of vector files, Map Authoring
* Common capabilities across the runtime
* Exposing more capabilities of the ArcGIS platform
* Better Mapping, Location APIs
* Easy platform sharing of maps and layers
* Much more symbology and renderers
* Many new layers, including Stream layers and Vector tiles
* Layers from local data now as well
* Raster function support
* KML support (Read immediately and Write in future)
* 2D maps and 3D scenes will have similar API
* Local Server for developers (should look into, they went over it too fast)
* Cross platform AppStudio, Xamarin
* Easy to consume Mobile Map Packages, better disconnected support
* iOS & Android released before User Conference
* Beta for Xamarin, Qt, Java, .Net will be released around the same time
* iOS & Android will support 3D by Q3
* Next year will have much more, Full motion video, Vector, Raster supports, advanced analysis, GeoAnalytics
* Better Loader support for asynchronously loading resources using the Loadable pattern
* Geometry will be **Immutable**

#### Loadable
* Simple state for checking status and monitoring
* No auto loading, must call ```load()``` explicitly
* Consistent pattern across all methods in their API
* Set props before loading resources for an easy way to configure AGS objects

#### Geometry API
* Synced across all platforms
* Better performance because of Immutability
* Can support curves (more compacted JOSN and more performant)
* Created with builders, e.g. Polygon Builder
* Now has spatial reference

#### Mapping API
* Map is now the central component
* Can use maps from ArcPro, Mobile Map Packages, Portal Items, Create from code and save locally or to Portal
* Creating from code has improved greatly
* MapView > Map > Layers
* Layers > FeatureLayer, RasterLayer, TiledLayer, MapImageLayer(formerly a DynamicMapServiceLayer)
* For 3D, Use SceneView. You can embed views in a GeoView
* GeoView is the parent class to MapViews and SceneViews
* GraphicsLayers are gone, Graphics Overlays replaces it, these are temporary in the application since Portal apparently does not and will probably not have support for saving Graphics layers, if you need to save them then you should use a FeatureLayer
* GeoView has the graphics overlays, draw events, location display, setViewpoint methods, and layer state events
* MapView has identify methods for graphics overlays and other layers (returns GeoElements), setViewpoint methods, visibility area change events
* Common ViewPoints to the JavaScript API
* Graphics have rendering modes to give better performance/UX, dynamic for better UX, static for better performance when their are lots of Graphics

#### The Map
* Operational Layers, Basemap, Spatial Reference (comes from first layer added), Initial Viewpoint, Bookmarks, Item (Portal or local)
* Needs spatial reference, min/max scale, and an initial viewpoint so the map can load (sometimes they can be derived from an added layer on the map)
* Update maps on portal or create and save map objects
* Really easy local saving and taking a map offline in Quartz 100 (100 is the release number of the final version)

#### Mobile Map Package
* Contains a list of maps, locator tasks, items, and path

#### Quartz Extras
* Tons of layer changes
* Feature Service enhancements for modes and pre-populating caches manually
* Features now implement Loadable, so we don't need OutFields, we don't need many query parameters, which allows the SDK to optimize feature queries for map rendering and you can request attributes and other metadata on an individual basis
* Layer Content interface can make it very easy to build legends and table of content widgets, even has content changed listeners
* Symbols are by reference, don't need explicit setters anymore
* Minor updates to the Portal API, but better logic for managing authentication (AuthenticationManager)
* AuthenticationManager streamlines issuing challenges and comes with UI so you don't need to worry about it
* AuthenticationManager handles tokens, creds, pki's, and can add custom Challenge handlers if you want to build a custom UI for the authentication.  In memory credential cache as well so they don't have to log in repeatedly and can save to keychain on some platforms

iOS Quartz
----------

#### Overview
* Supports iOS8 and Up
* Force Touch Support
* Generics
* Nullability annotations (must do this to extract value from optional)
* AuthenticationManager supports OAuth, auto syncing to keychain, and much more

#### Playground Support
```swift
import UIKit
import ArcGIS
import XCPlayground

let mapView = new AGSMapView(frame: CGRect(x: 0, y: 0, width: 300, height: 300))
let map = new AGSMap(basemap: AGSBasemap.imageryWithLabelsBasemap)

mapView.map = map

XCPlaygroundPage.currentPage.liveView = mapView
XCPlaygroundPage.currentPage.needsIndefiniteExecution = true
```

#### Swift
* Safer, faster, and more readable
* Currently Swift is not backwards compatible because it is so new
* Version 3.0 will be backwards compatible and at that point Swift will be in Quartz

#### iOS U/X
* Improved Popups
  * Inline Editing in Popups
  * Custom keyboards/views for various actions like email fields, date fields, phone number fields, etc.
  * Custom header/footer
  * Custom UI with PopupManagerClass which does all the business logic
  * reorder and hide sections
* Graphics Overlay can do 60fps with up to 25,000 features, big improvement over graphics layer
* Vector Basemaps are insanely fast
* Quartz Samples available in Swift inside a Universal App
* Integration with Auto Layout so you can handle responsive screen sizes and multi-tasking

Android Quartz
--------------

#### Overview
* Same benefits as other SDKs
* Gradle support and better dependency management, allows you to write custom build scripts in Groovy
* Bintray is a tool to simplify deployment

Java SDK
--------

#### Overview
* Same benefits as other SDKs
* JavaFX or Swing
* Cross platform (not mobile) with Windows, Linux, and OSX

Qt/QML SDK
----------

#### Overview
* Ability to access C++ api in JavaScript and QML
* New MapView and Map with new parameters to help get things more easily
* Many Improvements overall and will be using Qt 5.6
* QDoc for API Reference which means better documentation and access to API in Qt
* AppStudio will soon get the new Quartz SDK, is a breaking change and will require an update
* **Samples in Github**
  * Full samples and not just snippets
  * This needs to be investigated

#### Upcoming Features
* Webmap support
* Vector tiles
* Military symbology
* 3D support
* Mobile map package support

.Net SDK
--------

#### Overview
* Same benefits as other SDKs
* XAMARIN!!!
  * Pre-release possibly coming around end of March
  * Xamarin.Forms - Cross Platform UI Library
    * Less development time, more code sharing
    * Not the best when you need really custom UIs for each platform or platform-specific functionality
  * Xamarin.iOS and Xamarin.Android - Lets you build applications but requires more platform specific code
  * Xamarin Studio and Xamarin Android Player for all major OS's
  * Xamarin.iOS, Xamarin.Android, Xamarin.Forms all have the same API

**E-Mail:** dcardella@esri.com for slides in PDF form

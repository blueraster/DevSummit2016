Optimizing JavaScript Applications
==================================

#### Web Optimizer
* Custom Builds on jso.arcgis.com
* Use custom script to create dependency tree and generate esri module list
* Host it on CDN so it is available globally

#### Bower
* ```bower install arcgis-js-api```
* see recommended guide in github repo

#### Dojo Build system
* in packages you will need to ignore lots of moment stuff, see Rene's example
* Use feature flags with has to help code get eliminated with dead code elimination

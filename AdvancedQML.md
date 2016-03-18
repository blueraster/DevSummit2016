Advanced Qt/QML
===============

#### Handling Asynchronous Tasks
* C++ API uses signals and slots
* QML API has signal handlers

```
Task {
  id: task
  url: '...'

  function execute (params) {
    task.execute(params);
  }
}
Params {
  id: params
  where: '1 = 1'
  returnGeometry: true
}
```

#### Offline
* GeodatabaseSyncTask
* Make sure to set generateGeodatabaseParameters output spatial reference to the maps spatial reference
* TileCache ?? (forget the actual name but its for basemaps)
* QML very much can support disconnected mapping
* Enable Sync needs to be checked in ArcGIS Online
* Need to look into how to setup a sync enabled feature service

#### Aggregated Query Results
* OutStatistics can aggregate results from the same service
* Just goes into a normal Query as ```outStatistics```

#### Charts
* Can be used in C++ and in QML
* QML binding for Charts.js

#### Other
* Have a good way of handling security and authentication using oAuth
* Create a window in the app component that I can use anywhere to handle errors or status messages

```
//- This needs to be tested but they seem to use a similar workflow
//- Would be nice to apply slightly different styling to this component as well depending on the status
App {
  id: app

  Rectangle {
    id: messagingDialog

    Text {
      id: statusText
      text: 'Some Message'
    }
  }
}
messagingDialog.statusText.text = 'Error, something happened';
```

Questions
* Is there a good way in QML to monitor multiple async tasks and receive a signal when they have all completed?

-- Quick Promise in Github

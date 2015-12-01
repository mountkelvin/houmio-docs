The API is split into two parts: the configuration API (the "restful" part) and the control API (the Socket.io part).

# The REST API

`get /api/site/:siteKey` Get the configuration of the site.

`put /api/site/:siteKey` Update the site. Currently supports only changing the name.

`post /api/site/:siteKey/light` Create a new light.

`put /api/site/:siteKey/light` Update a light.

`delete /api/site/:siteKey/light/:lightId` Delete a light.

`post /api/site/:siteKey/scene` Create a scene.

`put /api/site/:siteKey/scene` Update a scene.

`delete /api/site/:siteKey/scene/:sceneId` Delete a scene.

`post /api/site/:siteKey/eventSource` Create an event source (typically, a button).

`put /api/site/:siteKey/eventSource` Update an event source.

`delete /api/site/:siteKey/eventSource/:eventSourceId` Delete an event source.

`post /api/site/:siteKey/schedule` Create a schedule.

`put /api/site/:siteKey/schedule` Update a schedule.

`delete /api/site/:siteKey/schedule/:scheduleId` Delete a schedule.

# The rest of the REST API

`put /api/site/:siteKey/scene/:sceneId/apply` Apply a scene.

# The Socket.io API

You can control your lights and scenes using our [Socket.io](http://socket.io/) API.

First, you might wan to get your site configuration as a reference for your light and scene ids, rooms and zones.

    curl https://houmi.herokuapp.com/api/site/yourSecretSiteKey
    
## Get started

Here's how to get started using Node.js and the `socket-io.client` npm module.

First install the module:

    npm install socket.io-client@1.3.6
    
Then try this:

```javascript
var io = require('socket.io-client')
var socket = io('https://houmi.herokuapp.com')
socket.on("connect", function() {
  console.log("connected")
  socket.emit('clientReady', { siteKey: "yourSecretSiteKey" })
  console.log("setting brightness")
  socket.emit('apply/light', {_id: "yourLightId", on: true, bri: 255 })
})
```

Remember to replace `yourSecretSiteKey` and `yourLightId` with real values!

## Commands

Following commands are supported:

    # Connect client
    > socket.emit('clientReady', { siteKey: "yourSecretSiteKey" })

    # Set light to given state
    > socket.emit('apply/light', {_id: "yourLightId", on: true, bri: 255 })

    # Apply scene
    > socket.emit('apply/scene', "yourSceneId")

    # Set all lights in zone to given state
    > socket.emit('apply/zone', { zone: "1st floor", on: true, bri: 255 })

    # Set all lights in room to given state
    # Note: if you do not use zones, specify zone: "".
    > socket.emit('apply/zone/room', { zone: "1st floor", "room": "kitchen", on: true, bri: 255 })

    # Set all lights to given state
    > socket.emit('apply/all', { on: true, bri: 255 })

## Events

Following events are supported:

    # Button and other source events
    socket.on('eventSourceKey', (event) -> console.log(event))
    
    # Changes to light states (on/off) and brightness
    socket.on('setLightState', (event) -> console.log(event))

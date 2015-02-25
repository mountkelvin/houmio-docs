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

# The Socket.io API

Get your site configuration as a reference for your light and scene ids, rooms and zones.

    curl https://houmi.herokuapp.com/api/site/yourSecretSiteKey

Open `https://houmi.herokuapp.com/site/yourSecretSiteKey` in Chrome. Open the JS console.

Following commands are supported:

    # Connect client
    > socket.emit('clientReady', { siteKey: "yourSecretSiteKey" }
    # Note: this is automatically emitted when opening https://houmi.herokuapp.com/site/yourSecretSiteKey

    # Set light to given state
    > socket.emit('apply/light', {_id: yourLightId, on: true, bri: 255 })

    # Apply scene
    > socket.emit('apply/scene', { _id: yourSceneId })

    # Set all lights in zone to given state
    > socket.emit('apply/zone', { zone: "1st floor", on: true, bri: 255 })

    # Set all lights in room to given state. Note: if you do not use zones, specify zone: "".
    > socket.emit('apply/zone/room', { zone: "1st floor", "room": "kitchen", on: true, bri: 255 })

    # Set all lights to given state
    > socket.emit('apply/all', { on: true, bri: 255 })

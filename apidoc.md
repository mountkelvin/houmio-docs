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

TODO

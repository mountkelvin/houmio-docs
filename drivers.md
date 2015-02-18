*In progress*

Writing custom drivers enables you to control devices which are not supported by Houm.io out of the box.

Your Houm.io Bridge has a bridge process which accepts tcp socket connections in port 3001.

After sending the `driverReady` message and receiving the `driverReadyAck` message, the bridge will send you `write` messages related to your protocol as one-liner serialized JSONs.

    nc localhost 3001
    > {"command": "driverReady", "protocol": "yourProtocol"}
    < {"command": "driverReadyAck"}
    < {"command":"write","protocol":"yourProtocol","data":{"_id":"54d2797057fe51112f56fa28","type":"dimmable","protocolAddress":"yourAddress","on":true,"bri":88}}
    < ...
    < ...

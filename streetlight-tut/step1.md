Let's start by creating an AsyncAPI file to describe your API. It will help you generate the code and the documentation later.

Copy below content to the editor, into `asyncapi.yaml` file:

<pre class="file" data-filename="asyncapi.yaml" data-target="replace">
    asyncapi: '2.0.0'
    info:
      title: Streetlights API
      version: '1.0.0'
      description: |
        The Smartylighting Streetlights API allows you
        to remotely manage the city lights.
      license:
        name: Apache 2.0
        url: 'https://www.apache.org/licenses/LICENSE-2.0'

    servers:
      mosquitto:
        url: mqtt://test.mosquitto.org
        protocol: mqtt

    channels:
      light/measured:
        publish:
          summary: Inform about environmental lighting conditions for a particular streetlight.
          operationId: onLightMeasured
          message:
            payload:
              type: object
              properties:
                id:
                  type: integer
                  minimum: 0
                  description: Id of the streetlight.
                lumens:
                  type: integer
                  minimum: 0
                  description: Light intensity measured in lumens.
                sentAt:
                  type: string
                  format: date-time
                  description: Date and time when the message was sent.
</pre>

Let's break it down into pieces:

```yaml
asyncapi: '2.0.0'
info:
  title: Streetlights API
  version: '1.0.0'
  description: |
    The Smartylighting Streetlights API allows you
    to remotely manage the city lights.
  license:
    name: Apache 2.0
    url: 'https://www.apache.org/licenses/LICENSE-2.0'
```

- The `asyncapi` field indicates you use AsyncAPI version 2.0.0.
- Inside the `info` field you find information about the API, like its name, version, description, and its license.

We're now going for the `channels` section. It is used to describe the event names your API will be publishing and/or subscribing to.

```yaml
channels:
  light/measured:
    publish:
      summary: Inform about environmental lighting conditions for a particular streetlight.
      operationId: onLightMeasured
```

In this example, `light/measured` is the channel name your API `publish` to. The `operationId` property, describes what will be the name of function or method that takes care of this functionality in generated code. To understand how the event should look like when publishing to that channel, there is the `payload` property:

```yaml
      payload:
        type: object
        properties:
          id:
            type: integer
            minimum: 0
            description: Id of the streetlight.
          lumens:
            type: integer
            minimum: 0
            description: Light intensity measured in lumens.
          sentAt:
            type: string
            format: date-time
            description: Date and time when the message was sent.
```

`Payload` property defines the content of the event using AsyncAPI schemas. It means that your event payload should contain an `id` and a `lumens` property —which are integers bigger than zero—, and a `sentAt` property that should be a string containing a date and time.

> JSON Schema Draft 07 is 100% compatible with AsyncAPI schemas.

Cool! So you're done with your AsyncAPI file! Let's get into generating code.
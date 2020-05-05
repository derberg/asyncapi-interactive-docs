To generate your code you'll use the [AsyncAPI Generator](https://github.com/asyncapi/generator) Node.js template.

# Generating code

1. Install the generator to use is at a command-line tool: `npm install -g @asyncapi/generator`{{execute}}

1. Trigger generation of the Node.js code: `ag asyncapi.yaml @asyncapi/nodejs-template -o output -p server=mosquitto`{{execute}}

1. And voilà! In the editor you can see a new folder is created with generated Node.js application. Enter the folder in the terminal: `cd output`{{execute}}

# Start your generated service

Install and start the service:

1. Install dependencies of newly generated application: `npm install`{{execute}}
1. Start the application: `npm start`{{execute}}

# Start MQTT broker

In this tutorial you use [Eclipse Mosquitto](https://mosquitto.org/) broker:

`docker run -it -p 1883:1883 -p 9001:9001 eclipse-mosquitto`{{execute T2}}

# Send a message to the broker

Use MQTT client to send a message to the broker you started in the previous step:

1. In another terminal install the MQTT.js library: `npm install mqtt -g`{{execute T3}}
1. Send message to your application: `mqtt pub -t 'light/measured' -h 'localhost' -m '{"id": 1, "lumens": 3, "sentAt": "2017-06-07T12:34:32.000Z"}'`{{execute}}

Go back to first terminal and notice that in your service logs you can see the message you just sent.

# Conclusions

You've learned how to create an AsyncAPI description file and how to generate code from it. The code is a bootstrap and you'll need to add your business logic into it. Take some time to play with it.
There are still lots of things to be covered but intent of this tutorial is to be simple so you get an idea of the potential.

We would also like to see what you create with AsyncAPI. As an open-source project, we're open to proposals, questions, suggestions, and contributions. If you don't feel in the mood to contribute but you're using AsyncAPI, just raise your hand [creating a issue in our Github repo](https://github.com/asyncapi/asyncapi/issues/new) or [join our Slack channel](https://www.asyncapi.com/slack-invite/). Don't be shy :)
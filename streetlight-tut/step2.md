To generate your code you'll use the [AsyncAPI Generator](https://github.com/asyncapi/generator) Node.js template.

# Generating code

1. Install the generator to use is at a command-line tool: `npm install -g @asyncapi/generator`{{execute}}

1. Trigger generation of the Node.js code: `ag asyncapi.yaml @asyncapi/nodejs-template -o output -p server=mosquitto`{{execute}}

1. And voilà! In the editor you can see a new folder is created with generated Node.js application. Enter the folder in the terminal: `cd output`{{execute}}

# Start your generated service

> This runs in main terminal

Install and start the service:

1. Install dependencies of newly generated application: `npm install`{{execute}}
1. Clear the terminal from all the previous noise `clear`{{execute}}
1. Start the application: `npm start`{{execute}}

# Start MQTT broker

> This runs in another terminal

In this tutorial you use [Eclipse Mosquitto](https://mosquitto.org/) broker:

`docker run -it -p 1883:1883 eclipse-mosquitto:1.5`{{execute T2}}

# Send a message to the broker

> This runs in yet another terminal. To see the message goes to your service logs check out the main terminal.

Use MQTT client to send a message to the broker you started in the previous step:

1. Install the MQTT.js library: `npm install mqtt@4.0.0 -g`{{execute T3}}
1. Send valid message to your application: `mqtt pub -t 'light/measured' -h 'localhost' -m '{"id": 1, "lumens": 3, "sentAt": "2017-06-07T12:34:32.000Z"}'`{{execute}}
1. Send invalid message to your application: `mqtt pub -t 'light/measured' -h 'localhost' -m '{"id": 1, "lumens": "3", "sentAt": "2017-06-07T12:34:32.000Z"}'`{{execute}}

Check the first terminal to see that your generated service received both messages but one was validated as incorrect. 

To generate your code you'll use the [AsyncAPI Generator](https://github.com/asyncapi/generator) Node.js template.
Make sure proper aliases are available: 
```
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```{{execute}}

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

1. Install the MQTT.js library: `npm install mqtt -g`{{execute T3}}
1. Send message to your application: `mqtt pub -t 'light/measured' -h 'localhost' -m '{"id": 1, "lumens": 3, "sentAt": "2017-06-07T12:34:32.000Z"}'`{{execute}}

Go back to first terminal and notice that in your service logs you can see the message you just sent.


https://[[HOST_SUBDOMAIN]]-1883-[[KATACODA_HOST]].environments.katacoda.com
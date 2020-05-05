In this tutorial, you get started with actual code and a (could-be) real-world use case. <!--more-->
Let's pretend you have a company called Smarty Lighting and you do smart-city lighting systems.

# System Description

You want to create a system capable of turning on/off the streetlights depending on the environmental conditions of each of them:

- You're going to implement an event-driven architecture, with a Message Broker in its "center".
- Streetlights will send information about its environmental lighting to the broker.
- None of the services waits for any kind of response. Think about it as _fire and forget_. You publish messages to the broker and that's it. Your service doesn't know who receives them.

# Technology

You'll use Node.js to code APIs and Mosquitto as the message broker. Selected technology is irrelevant here, as things explained here in this tutorial are applicable to any other programming language and message brokers.
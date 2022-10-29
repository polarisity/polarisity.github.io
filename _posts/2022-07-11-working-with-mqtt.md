---
title: "Working with MQTT"
date: 2022-07-11
---

I decided to set up an environmental monitoring device with my Spirulina farm. It uses the [enviro plus hat](https://learn.pimoroni.com/article/getting-started-with-enviro-plus) for raspberry pi. I decided to take this opportunity to work with GCP’s IoT Core and PubSub services. PubSub allows me to use the publisher subscriber model to connect various MQTT nodes together and allow me to work with my data flexibly. My first goal was to create a dashboard which would allow me to view my sensor data. Eventually, I would like to create a farming system for Spirlina.

There were two parts to this, getting the sensor data and sending the data to GCP.

Getting sensor data was easy, PiMoroni provides a [repository](https://github.com/pimoroni/enviroplus-python) with libraries and examples which are simple to install and use.

Sending data to GCP was harder. I didnt have much knowledge of MQTT. I started out with this [tutorial](https://cloud.google.com/community/tutorials/cloud-iot-enviro-board-workshop) and this [youtube video](https://www.youtube.com/watch?v=76v16P-Wqe4). I first tested out this [script](https://github.com/GoogleCloudPlatform/python-docs-samples/blob/main/iot/api-client/mqtt_example/cloudiot_mqtt_example.py) to get an idea of the parameters required. After which, I was able to reference several pieces of code such as [this](https://github.com/GoogleCloudPlatform/community/tree/master/tutorials/cloud-iot-enviro-board-workshop/enviro-device).

From what I understand, you first need your broker details. This comes in the form of a hostname and port. Once we have this, we will need a way to authenticate with the broker. Based on the tutorials above, the RSA key pair seemed like a simple solution. All that was left to configure the connection was the GCP IoT Core device ID, GCP project ID and PubSub topic.

I encountered problems while publishing messages though. My messages would not appear in PubSub. Interestingly, sending multiple messages improved reliability. While I was sending a single message, I was not able to see the messages appear in PubSub. After changing the number of messages to 4, the messages appeared. My current hypothesis is that the connection needs to be maintained in an open state. I’ll need further experiments to improve this.

Next, I will need to figure out how my raspberry pi can be set up to automatically startup and publish sensor data. After that, I will need to set up a pipeline with Cloud Functions and BigQuery which will allow me to view my sensor data.

---

Update: 13th July

Data seems to have stopped sometime last night. I’m unsure why this is happening as the script appeared to be running on login.

![]({{ site.baseurl }}/images/blog/2022-07-11-log.png)

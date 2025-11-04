# CS 5500 Project Description

## Learning Objectives

1. Gain software project management experience working as a software team using Scrum
2. Practice design patterns, clean code, and refactoring skills on a legacy codebase
3. Develop programming skills in Python, Bash, Linux, and API design
4. Learn how to use AI to help understand a codebase and aid in code development and develop relevant skills such as prompt engineering.   


## Project Description

Our sponsor is the Department of Energy. They maintain a software application called Volttron. It is used as a free and open-source application to help manage building energy usage. The application supports integration with various smart home devices such as Ecobee, which is a smart thermostat. The current maintainers originally built code to integrate Ecobee devices with Volttron. However it was last tested in 2019 and little work has been done to maintain it. Since that time, Ecobee has grown its user base to millions of residential customers in the US. There is significant growing interest on sustainability experts and hobbyists to integrate their Ecobee devices with the current version of Volttron.     

## Project Goal

Our goal for this project is to update the [Home Assistant Driver of Volttron](https://volttron.readthedocs.io/en/releases-9.x/agent-framework/driver-framework/home-assistant/HomeAssistantDriver.html#). Home Assistant is an open-source application that allows a user to manage and control Home Assistant-compatible devices within their building (e.g. residential house).

The Home Assistant has a limitation on its write-access functionality on various devices. The documentation states that "Currently control(write access) is supported only for lights(state and brightness) and thermostats(state and temperature)." Our goal is to extend write-access functionality beyong lights and thermostats and support other devices. Our overall goal can be decomposed into three high level goals:

1. Expand the write access functionality of the Home Assistant Driver to more devices 
2. Update integration tests and documentation for Home Assistant Driver
3. Stretch Goal: Test the expanded functionality on a real Home Assistant device (requires IP address and API Key) 

References:
* [Home Assistnant API](https://developers.home-assistant.io/docs/api/rest)
* [Home Assistant Entity Object]([https://developer.ecobee.com/home/developer/api/introduction/index.shtml](https://developers.home-assistant.io/docs/core/entity))
* [Home Assistant Driver — VOLTTRON 9.0.4 documentation](https://volttron.readthedocs.io/en/releases-9.x/agent-framework/driver-framework/home-assistant/HomeAssistantDriver.html#)
* [Home Assistant Driver agent class](https://github.com/cs5500-neu/volttron/blob/main/services/core/PlatformDriverAgent/platform_driver/interfaces/home_assistant.py)

## What is Volttron

VOLTTRON™ is an open source, scalable, and distributed platform that seamlessly integrates data, devices, and systems for sensing and control applications. It is built on extensible frameworks allowing contributors to easily expand the capabilities of the platform to meet their use cases. Features are implemented as loosely coupled software components, called agents, enabling flexible deployment options and easy customization.

[VOLTTRON™ documentation! — VOLTTRON 9.0.4 documentation](https://volttron.readthedocs.io/en/main/index.html)

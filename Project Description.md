# CS 5500 Project Description

## Learning Objectives

1. Gain software project management experience working as a software team using Scrum
2. Practice design patterns, clean code, and refactoring skills on a legacy codebase
3. Develop programming skills in Python, Bash, Linux, and API design
4. Learn how to use AI to help understand a codebase and aid in code development and develop relevant skills such as prompt engineering.   


## Project Description

Our sponsor is the Department of Energy. They maintain a software application called Volttron. It is used as a free and open-source application to help manage building energy usage. The application supports integration with various smart home devices such as Ecobee, which is a smart thermostat. The current maintainers originally built code to integrate Ecobee devices with Volttron. However it was last tested in 2019 and little work has been done to maintain it. Since that time, Ecobee has grown its user base to millions of residential customers in the US. There is significant growing interest on sustainability experts and hobbyists to integrate their Ecobee devices with the current version of Volttron.     

## Project Goal

Our goal for this project is to update the Ecobee Driver of Volttron which was last tested in 2019. The Ecobee API's have significantly changed since then. Our goals are three-fold:

1. Update the Ecobee Driver to work with the latest Ecobee API's 
2. Update any tests and documentation for Ecobee
3. Stretch Goal: Add a new feature to the Ecobee Driver 

References:
* [ecobee API](https://developer.ecobee.com/home/developer/api/introduction/index.shtml)
* [Ecobee Driver — VOLTTRON 9.0.4 documentation](https://volttron.readthedocs.io/en/main/agent-framework/driver-framework/ecobee/ecobee-web-driver.html) 

## What is Volttron

VOLTTRON™ is an open source, scalable, and distributed platform that seamlessly integrates data, devices, and systems for sensing and control applications. It is built on extensible frameworks allowing contributors to easily expand the capabilities of the platform to meet their use cases. Features are implemented as loosely coupled software components, called agents, enabling flexible deployment options and easy customization.

[VOLTTRON™ documentation! — VOLTTRON 9.0.4 documentation](https://volttron.readthedocs.io/en/main/index.html)

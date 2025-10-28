# Development Environment Setup for Volttron

## How to Install Ubuntu on VirtualBox 

NOTE: Instructions are for Apple Silicon Macbooks. If using an Intel-based Macbook. please download the Intel-based versions of the software mentioned in Prerequisites. 

If using a Windows machine, refer to [these instructions](https://www.youtube.com/watch?v=dKJ3Wee8w9w)

## Prerequisites

* Download latest version of VirtualBox
  * [Download Link](https://www.virtualbox.org/wiki/Downloads) 
  * For Apple Silicon Mac, download the ARM64 Version
  
* Download latest version of Ubuntu Desktop
  * [Download Ubuntu Desktop \| Ubuntu](https://ubuntu.com/download/desktop)
  * For the Apple Silicon Mac, download the ARM64 version, [here](https://cdimage.ubuntu.com/ubuntu/releases/noble/release/ubuntu-24.04.3-desktop-arm64.iso)
  * Link to the mirror [download library for version 24.03](https://cdimage.ubuntu.com/ubuntu/releases/noble/release/)

## Install VirtualBox

1. Double-click the VirtualBox DMG file.
1. Open the installer and follow the on-screen instructions.

## Install Ubuntu on VirtualBox

NOTE: Instructions for Apple Silcon Mac and Virtual Box version 7.2.4. If using Intel-based Mac, use the AMD64 (x86-64) version.

1. Click New in VirtualBox and give a name to the VM.
1. Set `OS Image` to the downloaded ISO image of the Ubuntu image that you downloaded in Prerequisites.
1. Uncheck `Proceed with Unattended Installation` 
1. Check that the following are configured under the `Virtual machine name and operating system` tab: 
   * `OS` set to `Linux`
   * `OS Distribution` set to `Ubuntu`
   * `OS Version` set to `Ubuntu ARM 64 Bit`
1. Expand `Specify Virtual Hardware` tab, allocate at least 4096 MB (4 GB) for Base Memory (i.e. RAM) and 4 CPU cores for smooth performance.
1. Click Finish
1. Right click your new VM on the VirtualBox console and select `Settings`
1. Click `Display` on the right side, under `Scren`, set `Video Memory to maximum limit (usually 128 MB)`
1. Change`Graphics Controller` to `VBoxSVGA`
1. Click `OK`
1. Start the VM. It should open a new window
1. Click `Install Ubuntu` icon
1. Follow installation instructions
1. After the initial installation, click the `Install Ubuntu` icon on the Desktop (usually at the right side). 
1. Follow the installation instructions again
1. After installation, click `Restart Now`
1. Press `Enter`
1. Log in to the VM
1. Open a `Terminal` application
1. Run `sudo apt update`
1. Run `sudo apt install git vim openssh-server`
1. Run `sudo systemctl status ssh`; notice the status set to inactive. We need to set this to running. 
1. Run `sudo systemctl start ssh`
1. Run `sudo systemctl enable ssh`
1. Run `sudo systemctl status ssh`; verify that the app is now `running` and `enabled`. This configuration will allow you to `ssh` into the VM using your terminal on your host machine and not have to open a GUI. 
1. Poweroff the VM
1. Right click the VM on the VirtualBox console. 
1. Expand the `Network` tab on the left
1. Under `Adapter 1`, click the `Port Forwarding` and add a new `Port Forwarding` rule
1. Set Name to `SSH`
1. Set `Host Port` to `2222`
1. Set `Guest Port` to `22`
1. Start the VM without the GUI (ie Headless mode)
1. Open a terminal on your local machine; your goal is to access the VM without using GUI and instead use the command line. Run the following: `ssh -A <username>@127.0.0.1 -p 2222` You are now in the VM.

## Install Volttron 

1. Fork the Volttron repo from [GitHub - cs5500-neu/volttron: VOLTTRON Distributed Control System Platform](https://github.com/cs5500-neu/volttron)
2. Now that your team has a forked repo, clone the team's forked repo onto your VM and NOT on your local machine. Ensure that you open a terminal and SSH into your VM.
3. Install these dependencies: `sudo apt install gcc python3-dev install python3.12-venv`
4. Navigate to your `volttron` folder
5. Install volttron : `python3 bootstrap.py --drivers --force`
6. Activate the virtual environment: `source env/bin/activate`
7. Start Volttron: `./start-volttron`
8. Check Volttron is running: `vctl status`
9. Stop Volttron: `./stop-volttron`

## Setup your IDE to connect to the VM

To easily develop working code on your VM, connect your IDE to the VM via SSH. 

For example, if you are using Visual Studio Code, click the blue bottom left corner and select `Connect Current Window to Host`  and then select `Add New SSH host` option on the dropdown. Copy and paste your `ssh` command that you used to access the VM through the command line. It should take the form of `ssh -A <username>@localhost -p 2222`. Press enter to update your ssh config file and then hit Connect. Enter your password for your user if required. Your Visual Studio Code window that has access to all the files and folders on your VM. Open the folder containing your forked version of Volttron. Now going forward, you can make changes to the application and test it out directly on your VM. 


## Using Volttron

Volttron is primarily managed through the terminal. All commands are run inside a virtual Python environment. When installing the agents, ensure that you navigate to the root 
of your repo. 

### Installing Agents

First, ensure that you activate your virtual environment. Navigate to the root of your repo and run:

`source env/bin/activate`

Installation requires that Volttron has started and is running. Navigate to the root of the repo and run the command:

`./start-volttron`

Alternatively, you can start Volttron anywhere on the machine with the following command:

`volttron -vv -l volttron.log&`


#### Install a Listener Agent

Read: [Listener Agent — VOLTTRON 9.0.4 documentation](https://volttron.readthedocs.io/en/develop/developing-volttron/developing-agents/example-agents/listener-agent.html)

Install the agent: `vctl install examples/ListenerAgent`

Check the status: 

`vctl status`

This will output the agent information as so:

```
UUID AGENT                    IDENTITY            TAG STATUS          HEALTH
6e listeneragent-3.3        listeneragent-3.3_1
```

Notice the UUID of this agent and its status. The agent has not started. Start it by running the following command and using the agent's UUID:

`vctl startt 6e`

Follow this same pattern for starting the other agents in this tutorial.

#### Install a Platform Driver

Read [Platform Driver — VOLTTRON 9.0.4 documentation](https://volttron.readthedocs.io/en/main/agent-framework/driver-framework/platform-driver/platform-driver.html#)

Install the agent: `vctl install services/core/PlatformDriverAgent --config services/core/PlatformDriverAgent/platform-driver.agent --vip-identity platform.driver`


Start the agent; see example of how an agent is started in the Install Listener Agent section. 

#### Install a Fake Driver

Read [Fake Driver — VOLTTRON 9.0.4 documentation](https://volttron.readthedocs.io/en/9.0.4/agent-framework/driver-framework/fake-driver/fake-driver.html)

Installing a Fake Driver or any driver that implements the Driver Framework requires some additional steps and is different from how agents are usually installed. It requires the Platform Driver Agent to be installed first. 

Refer to [Fake Driver — VOLTTRON 9.0.4 documentation](https://volttron.readthedocs.io/en/9.0.4/agent-framework/driver-framework/fake-driver/fake-driver.html#installation) on installing a Fake Driver. 

Or follow these steps:

0. Navigate to the root of the repo
1. Stop the Platform Driver agent:`vctl stop <UUID of Platform Driver Agent`
2. Run `mkdir config`
3. Copy fake config to config: `cp examples/configurations/drivers/fake.config config/` 
4. Copy fake data file to config: `cp examples/configurations/drivers/fake.csv config/`
5. Add the files to the Config Store: `vctl config store platform.driver devices/campus/building/fake config/fake.config` and `vctl config store platform.driver fake.csv config/fake.csv --csv`
6. Start the Platform Driver agent and Listener Agent
7. View the logs in `volttron.log` which is located in the root level of your repo. You should see data being displayed from the Listener Agent, which is listening to all data being sent to the Message Bus. 



#### Install an SQL Historian

Read: [SQLHistorian — VOLTTRON 9.0.4 documentation](https://volttron.readthedocs.io/en/develop/volttron-api/services/SQLHistorian/README.html)

Install an SQL Historian that uses sqlite as its database. 

Install the prerequisite sqlite3: `sudo apt install sqlite3`

On your own, install and start an SQL Historian agent that uses an sqlite database. 


## Troubleshooting

* If you don't shutdown Volttron correctly, then you might not be able to restart it because the port that Volttron needs to use is already in use by another program, most likely the old Volttron that you didn'd shutdown correctly. If this happens, find the volttron process that is still running and manually kill it: 

```
ps -A | grep volttron`

# outputs something like:  6899 pts/0    00:00:00 volttron
# use the PID number on the left and kill it

kill -9 6899
```





# tb3-ros

## Intro

This is a docker package to allow you to run ROS and related applications through your browser. The following is installed:

* ROS Melodic
* Turtlbot3 packages
* prrexamples: examples from the book Programming Robotis with Ros
* Gen5: Assignments for this generation of Cosi119a
* Here are some handy commands for later: https://campus-rover.gitbook.io/lab-notebook/ros-tips/handy-commands

## Instructions

### Installation

* Install on your computer by cloning this github repo
* Currently supported on mac with some testing 
* Linux has had no testing

#### Mac Install
* Install Docker for Mac. See [instructions](https://hub.docker.com/editions/community/docker-ce-desktop-mac/)
* Clone this repo
  ```bash
  git clone https://github.com/pitosalas/tb3-ros.git
  ```

#### Windows Install
* Install Docker for Windows. See [instructions](https://hub.docker.com/editions/community/docker-ce-desktop-windows/)
* Clone this repo
* Once Docker is installed, go to `Settings` -> `Resources` -> `File Sharing`
  * Check the "+" sign and add the directory of this repo, i.e `C:\Users\Robot\Documents\tb3-ros`

### Launching it

#### Mac Launch
* Start the container
  ```bash
  make start
  ```
* Stop the container
  ```bash
  make stop
  ```

#### Windows Launch
*Using Powershell*
* Start the container
  ```powershell
  .\win-make start
  ```
* Stop the container!
  ```powershell
  .\win-make stop
  ```

#### Server mode

`tb3-ros` supports a server mode where multiple instances of this image are created in the same server. **Only available on linux**

##### Requirements

Before you use server mode, there are a couple things you will need:

- On the host machine/server:
  - Ruby > 2.6
  - `make`
- Tailscale [Authkey](https://login.tailscale.com/admin/authkeys)

Before starting the server, use `generate.rb` to generate a new `docker-compose.yaml` file.

```bash
# ruby generate.rb <container_names>
ruby generate.rb apple orange melon
```

To start the containers,

```bash
# AUTHKEY  Tailscale AuthKey     i.e. tskey-123abc...
# ROUTES   Docker subnet network i.e. 172.31.0.0/16
# GW_IP    Docker subnet gateway i.e. 172.31.0.1
# RELAY_IP Tailscale-relay IP    i.e. 172.31.0.2
AUTHKEY=<Tailscale Authkey> ROUTES=<Subnet Network> GW_IP=<Subnet Gateway> RELAY_IP=<Tailscale-relay IP> make start-server
```

To restart specific container,

```bash
make restart-server containers="apple orange"
```

### Accessing the virtual desktop
* Browser: http://0.0.0.0:6080/vnc.html
* Click on desktop and get a tiny menu. Click "terminal"
* In that terminal do `source setup.bash`
* Now click on desktop and get a second terminal with a legible font

### Accessing a virtual instance of VSCode for coding

* VSCode is a very popular text editor
* You can get to it with http://0.0.0.0:80
* If it asks for a password, use `dev@ros`

### Setup SSH for remote access
* To enable ssh, first login using virtual desktop/VScode
* Open up the terminal
* Run `sudo passwd root` to setup a password
* To SSH in: `ssh root@host -p 222n`, type in the previous password

## Playing around

* If you don't know much about ROS but want to see what it's like, try these commands
* Open a terminal window and do: `roscore`
* Open a different terminal window and do: `roslaunch turtlebot3_fake turtlebot3_fake.launch`
* Open a different terminal window and do: `roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch`


## Working with the container

### Start container

```bash
make start
```

### Stop container

```bash
make stop
```

### Fix any issues introduced by force-stop

```bash
make fix
```

### Rebuild the image

*Only used when developing this image.* 

If you want want the latest version of `tb3-ros`, do a `docker pull cosi119/tb3-ros:latest` instead.

```bash
make build
```

### Fixing the REST error

```bash
sed -i -e 's/https:\/\/api.ignitionfuel.org/https:\/\/api.ignitionrobotics.org/g' ~/.ignition/fuel/config.yaml
```

## Access IDE
http://0.0.0.0:80
password is: `dev@ros`

## Access linux to run graphical programs
http://0.0.0.0:6080/vnc.html
password is: `dev@ros`

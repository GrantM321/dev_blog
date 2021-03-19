---
title: "Drone Update"
date: "2021-03-19"
---

## The Goal
 The Goal for this sprint was to make some good progress on the backend for the drones now that we have a good idea of what we are working towards. 

## The Process
At first we were going strongly through our Kanban board, we were completing important tasks at a solid pace to good effect. 
One of the tools we used and will continue to use is a github repository that contains many examples of code that could be used to fly the drones. 

![A screenshot of the Github Repo]({{site.url}}/assets/github-repo.png)
This is a screenshot of the repo that we use for ideas, such as an interval that sends commands multiple times in a short amount of time. 

More things we looked at from the repo was the exchanger, a list of commands, and a constants page. 

```Javascript
const dgram = require('dgram'),
    client = dgram.createSocket('udp4'),
    constants = require('./constants.json'),
    _local = {
        state: "idle"
    }

client.on('message', (msg,info) => {
    _local.state = msg.toString()
}); 

client.bind(constants.ports.response)

const bindStateManagement = (resolve, reject) => {
    let timeoutId = setTimeout(() => {
        _local.state = "error"
    }, 10000);
    let intervalId = setInterval(() => {
        if(isIdle())
            return
        if(isError())
            reject(_local.state)
        else
            resolve(_local.state)
        clearInterval(intervalId)
        clearTimeout(timeoutId)
        _local.state = "idle"
    }, 100);
}

const isIdle = () => _local.state === "idle"
const isError = () => _local.state === "error"

const transmit = (command) => {
    const message = Buffer.from(command)
    client.send(message, 0, message.length, constants.ports.command, constants.hosts.remote, (error) => {
        if(error)
            _local.state = "error"
    })
}

const send = (command) => {
    return new Promise((resolve, reject) => {
        if(!isIdle())
            reject("error")
        bindStateManagement(resolve,reject)        
        transmit(command)
    })
}

module.exports = { send, _local }
```
This is the code for the exchagner part of the repo. This basically checks to see if the drone is idle and ready for a command, or if the drone is not responding, and sets the state to error if nothing happens after a bit. 

``` Javascript
{
    "hosts": {
        "remote": "192.168.10.1",
        "local": "0.0.0.0"
    },
    "ports":{
        "command": 8889,
        "response": 8001,
        "state": 8890,
        "video": 11111
    }
}

```
This is an example of constants from the repo on github, ours has a drone and server hosts instead of remote and local. For the ports we only have one at the moment, and it is command. 

``` Javascript
const commander = require('../exchanger')

const connect = () => commander.send('command')

const takeOff = () => commander.send('takeoff')

const land = () => commander.send('land')

const emergency = () => commander.send('emergency')

const stop = () => commander.send('stop')

const flip = (side) => commander.send(`flip ${side}`)

const up = (distance) => commander.send(`up ${distance}`)

const down = (distance) => commander.send(`down ${distance}`)

const left = (distance) => commander.send(`left ${distance}`)

const right = (distance) => commander.send(`right ${distance}`)

const front = (distance) => commander.send(`forward ${distance}`)

const back = (distance) => commander.send(`back ${distance}`)
```
This is an example of the commands that are set up in the repo, we will have some of these as all of them will not be needed. 


After looking at the repo for examples, we started to check out how the curve command works.
Good news: It worked!
Bad news: Our emergency command did not, and our drone got stuck on a light. 


## The Roadblocks

We are quite stuck. It seems that after every error we fix, another one pops up right after. We have had some ah-ha moments such as forgetting that we had to export our code so we could import it, or figuring out how curves work. Despite these errors, we intend on making more progress next week and breaking through these blocks. 




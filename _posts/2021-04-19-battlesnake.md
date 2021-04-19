---
title: "Battlesnake competition"
date: "2021-04-19"
---

## The project

Over the past couple of weeks we have been learning how to code a battle snake with javascript. Our goal was to attempt different challenges and to compete with each other in a tournament. 
Over this time period, we began to understand what we needed to do bit by bit. We first started to make it detect and avoid walls, then we tried to make it avoid running into itself, and finally we tried to make it get food. 

# My role 
My teammate and I did not really have specific roles, we just both worked on code at the same time. We would help each other when we ran into issues and bugs and give each other advice. We did it this way because we thought it would be faster. 

# Our thinking 
I think that thinking algorithmically is to think in an order, one step at a time. This is how we thought throughout this project. For example, we only looked at one problem at a time, such as running into walls, or looking for food. 

# The results 
Our snake did not do too well. We were second to be taken out of the competition, and we had very low scores in the challenges, and those scores were from the starter code we used because our snake was not working. 
```` javascript
  module.exports = {
    canMoveLeft: (head) => {
        if (head.x == 0) {
            return true
        } else {
            return false
        }
    },

    canMoveRight: (head) => {
      if (!head.x == board.width - 1) {
        return true
      } else {
        return false
      }
    },

    canMoveUp: (head) => {
        if (!head.y == board.height - 1) {
            return true
        } else {
            return false
        }
    },

    canMoveDown: (head) => {
        if (!head.y == 0) {
            return true
        } else {
            return false
        }
    },

    dontMoveBackwards: (head, neck) => {
      if (!head.y == neck.y + 1 || head.y == neck.y - 1 ||
       head.x == neck.x + 1 || head.x == neck.x - 1) {
         return false 
       } else {
         return true
       }
    }
````
This is an example of what we tried to do. We tried to make functions to return a state in certain senarios. 

```` Javascript 
const bodyParser = require('body-parser')
// const express = require('express')
// const routes = require('./lib/routes.js')

// const PORT = process.env.PORT || 3000

// const app = express()
// app.use(bodyParser.json())

// app.get('/', routes.handleIndex)
// app.post('/start', handleStart)
// app.post('/move', handleMove)
// app.post('/end', handleEnd)

// app.listen(PORT, () => console.log(`Battlesnake Server listening at http://127.0.0.1:${PORT}`))

// // function handleIndex(request, response) {
// //   var battlesnakeInfo = 
// //   {
// //     apiversion: config.apiversion,
// //     author: config.apiversion,
// //     color: config.apiversion,
// //     head: config.apiversion,
// //     tail: config.apiversion
// //   }
// //   response.status(200).json(battlesnakeInfo)
// // }

// function handleStart(request, response) {
//   var gameData = request.body

//   console.log('START')
//   response.status(200).send('ok')
// }

// function handleMove(request, response) {
//   var gameData = request.body

//   var possibleMoves = ['up', 'down', 'left', 'right']
//   var move = possibleMoves[3]
//   console.log(gameData.food)
//   console.log(gameData.board.height)
//   console.log(gameData.board.width)
//   console.log(gameData.you)
//   var head = gameData.you.head

//   if (!moves.canMoveLeft(head)) {
//     possibleMoves = possibleMoves.filter(move => move != "left")
//   }

//   if (!moves.canMoveRight(head)) {
//     possibleMoves = possibleMoves.filter(move => move != "right")
//   }

//   if (!moves.canMoveUp(head)) {
//     possibleMoves = possibleMoves.filter(move => move != "up")
//   }


//   if (!moves.canMoveDown(head)) {
//     possibleMoves = possibleMoves.filter(move => move != "down")
//   }

//   var move = possibleMoves[Math.floor(Math.random() * possibleMoves.length)]

//   console.log('move:' + move)
//   response.status(200).send({
//     move
//   })
// }

// function handleEnd(request, response) {
//   var gameData = request.body

//   console.log('END')
//   response.status(200).send('ok')
// }

// \/\/\/\/\/\/\/\/\/\/\/\/\/\/\/\/\/\/\/\/\/\/\/\/\/\/\/\/\\
````
This is what we had in our index. If the functions returned a certain state, they would remove the move that would kill it from the possible ways it could move, then it would move in a random direciton.
This is not what happened however, because the snake would either go up until it hits the top, or down until it hits the bottom. 

![Snake action](https://exporter.battlesnake.com/games/74892871-f395-41cf-a0c6-0dbcc7f81560/gif)
This is what our snake was able to do.

# What we learned
We learned that taking a bigger problem and dividing it into smaller ones is a very effective way to solve problems. Despite our efforts to do this, we still should have broken the problems down even more. For example, we tried to stop our snake from hitting all of the walls at once instead of doing them one at a time. I think this is one of the main reasons that we did not succeed in a lot of the challenges. 

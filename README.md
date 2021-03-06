# NodeJS Project: Snake Game

## Table of contents
* [General info](#general-info)
* [Technologies](#technologies)
* [Setup](#setup)
* [Code Explanation](#code-explanation)
  - [Index js](#index-js)
  - [Index.html](#index.html)
  - [Singlephase.js](#singlephase.js)
  - [MainScene.js](#mainscene.js)
  - [Snake.js](#snake.js)


## General info
This project is a Single player Snake Game using Node.js
	
## Technologies
Project is created with:
* Node.js version: 16.13.2
* Express version: 4.17.2
* CDNJS Phaser libraries Game framework
	
## Setup
To run this project, install it locally using npm:

```
$ cd ../SnakeGame_nodeJs
$ npm install
$ npm start
$ npm i express
```
## Code Explanation
### Index.js
```
const express = require('express');  
```
Imports an express module
```
const app = express();
```
Express() returns a JavaScript function, designed to be passed to Node’s HTTP servers as a callback to handle requests.
```
const port = 3000;
```
creates a port at 3000
```
app.use(express.static(__dirname + '/public/'));
```
Given the location of the html file to be executed on the browser.
```
app.get('/', (req, res) => res.sendFile('index.html'));
```
The Express application uses a callback function whose parameters are request and response objects.

Request Object represents the HTTP request and has properties for the request query string,parameters,body,HTTP headers and so on.  
Response Object represents the HTTP response that an Express app sends when it gets an HTTP request.  
Printing req and res provides information such as cookies, sessions, URL,etc.  
```
app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```
Binds and listens the connections on the Host and Port. 

A JavaScript function, designed to be passed to Node’s HTTP servers as a callback to handle requests.  
Entire Code for index.js
```
const express = require('express');
const app = express();
const port = 3000;

app.use(express.static(__dirname + '/public/'));
app.get('/', (req, res) => res.sendFile('index.html'));

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```
### Index.html

Create a public folder and create new html file named 'index'.  

```
<script type="module" src= "js/singlephase.js"></script>
```
We specify the type as 'module' as the import declaration appears at the top level of a module.  

Complete index.html code is as follows.  
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/phaser/3.60.0-beta.3/phaser-arcade-physics.js" integrity="sha512-BZJwCaPXDg0z5yA1Iiusrnwppw0WrSSVcuu38hcxLZ4/ehZyDPbhF8VeuaoATpaQ3cApef0NIBUvuZufolfhfA==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
    <title>Single Player Phaser Game</title>
</head>
<body>
    <h1>Single Player Phaser Game</h1>
    <div id= "phaser-game"></div>
    <script type="module" src= "js/singlephase.js"></script>
</body>
</html>
```
### Singlephase.js
Create a JS folder inside Public directory.  
This basically is a canvas in which our game will be placed.

```
    width: 640,
    height: 640,

```
Setting the game space width and height.
```
 type: Phaser.AUTO,
```
We set Phaser to decide automatically what type of game space to use.
```
parent: 'phaser-game',
```
This is where the game will be placed.It is the id we used under div tag in html file.
```
 scene: [MainScene]
```
This is where all our scenes will be added. It is an array, containing all scenes defined in MainScene class.  

```
new Phaser.Game(config);
```
We create new phaser game object and pass config to it.  

Complete singlephase.js file code is as follows.
```
import MainScene from "./MainScene.js";
const config = {
    width: 640,
    height: 640,
    type: Phaser.AUTO,
    parent: 'phaser-game',
    scene: [MainScene]
};

new Phaser.Game(config);
```
### MainScene.js
Holds the snake game code  

```
export default class MainScene extends Phaser.Scene {
```
We create a class MainScene  

```
constructor() {
        super('MainScene');
    }
```
We create a constructor.    
The super keyword is used to access and call functions on an object's parent, here 'MainScene'.  

```
create() {
        this.snake = new Snake(this);
    }
```
This is used at the beginning to initialise the scene.  

```
update(time){
        this.snake.update(time);
    }
```
This is used to update the scene from time to time.  

Complete MainScene.js file code is as follows
```
import Snake from './Snake.js';

export default class MainScene extends Phaser.Scene {
    constructor() {
        super('MainScene');
    }
    create() {
        this.snake = new Snake(this);
    }

    update(time){
        this.snake.update(time);
    }
}
```

### Snake.js
Complete Snake.js file code is as follows
```
export default class Snake {
    constructor(scene){
        this.scene = scene;
        this.box = this.scene.add.rectangle(0,0,16,16,0xff0000).setOrigin(0);
    }
    update(time){
        this.box.x += 1;
    }
}
```

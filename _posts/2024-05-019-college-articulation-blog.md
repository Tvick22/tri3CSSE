---
comments: false
layout: post
title: College Articulation Blog
description: Each student will build Chapters of their GitHub Pages College Articulation Blog. It is expected that you have Chapters on JavaScript Objects, Finite State Machines using Objects, and Single Requirements Principles in Coding Methods.
type: ccc
courses: { csse: { week: 7 } }
---

## Game Control Code: <label for="total-grade">Total: </label> <select><option>0</option><option>1</option><option>2</option><option>3</option><option>4</option><option>5</option><select> / 5, <label for="total-grade">Grade: </label> <select><option>0</option><option>1</option><select> /1

---

Starting with GameSetup you will describe the JavaScript Objects and how they are collected:

#### *GameSetup.js*

```js
skibidiToilet: {
    src: "/images/platformer/sprites/skibidiEnemy.png",
    width: 529,
    height: 884,
    scaleSize: 60,
    speedRatio: 0.85,
},
skibidiTitan: {
    src: "/images/platformer/sprites/skibidiTItan.png",
    width: 529,
    height: 884,
    scaleSize: 1500,
    speedRatio: 0.85,
},
```

#### **skibidiToilet** & **skibidiTitan** are assests that define the src, width, height, scaleSize, and speedRatio of the enimies

#### *GameSetup.js*

```js
const skibidiGameObjects = [
    { name: 'desert', id: 'background', class: Background, data: this.assets.backgrounds.desert },
    { name: 'skibidiTitan', id: 'skibidiTitan', class: skibidiTitan, data: this.assets.enemies.skibidiTitan, xPercentage:  0.35, minPosition: 0.5 }, 
    { name: 'sand', id: 'platform', class: Platform, data: this.assets.platforms.sand },
    { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.2, yPercentage: 1 },
    { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.4, yPercentage: 0.6 },
    { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.325, yPercentage: 0.8 },
    { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.2, yPercentage: 0.5 },
    { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.225, yPercentage: 0.5 },
    { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.0, yPercentage: 0.5 } ,
    { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.025, yPercentage: 0.5 },
    { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.025, yPercentage: 0.5 },
    { name: 'coin', id: 'coin', class: Coin, data: this.assets.obstacles.vbucks, xPercentage: 0.325, yPercentage: 0.7 },
    { name: 'coin', id: 'coin', class: Coin, data: this.assets.obstacles.vbucks, xPercentage: -0.0125, yPercentage: 0.4 },
    { name: 'coin', id: 'coin', class: Coin, data: this.assets.obstacles.vbucks, xPercentage: 0.0125, yPercentage: 0.4 },
    { name: 'coin', id: 'coin', class: Coin, data: this.assets.obstacles.vbucks, xPercentage: 0.0325, yPercentage: 0.4 },
    { name: 'SkibidiToilet', id: 'SkibidiToilet', class: SkibidiToilet, data: this.assets.enemies.skibidiToilet, xPercentage:  0.3, minPosition: 0.07 },
    { name: 'SkibidiToilet', id: 'SkibidiToilet', class: SkibidiToilet, data: this.assets.enemies.skibidiToilet, xPercentage:  0.5, minPosition: 0.3 },
    { name: 'SkibidiToilet', id: 'SkibidiToilet', class: SkibidiToilet, data: this.assets.enemies.skibidiToilet, xPercentage:  0.75, minPosition: 0.5 },
    { name: 'escaper', id: 'player', class: PlayerSkibidi, data: this.assets.players.escaper  },
    { name: 'laser', id: 'Laser', class: Laser, data: this.assets.obstacles.laser, xPercentage:  0.75, yPercentage: 0.5 },
    { name: 'toiletTube', id: 'toiletEnd', class: Tree, data: this.assets.obstacles.toilet },
    { name: 'complete3', id: 'background', class: BackgroundTransitions,  data: this.assets.backgrounds.complete3 },
];
```

## Class Design using DrawIO - <label for="total-grade">Total: </label> <select><option>0</option><option>1</option><option>2</option><option>3</option><select> / 3, <label for="total-grade">Grade: </label> <select><option>0</option><option>1</option><select> /1

---

Illustrate the design of GameObjects. Consider how Player, Enemy, and other Obstacles are all GameObjects.
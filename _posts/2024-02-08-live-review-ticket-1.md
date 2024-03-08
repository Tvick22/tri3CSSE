---
title: Live Review
comments: false
layout: post
description:Instructions: You will have 15 minutes before we start for review. You will plan to share with me as a triangle together for about 3 minutes (~1 minute per person).  Simply review what you did very quickly. Post an issue at the bottom of this page (https://github.com/orgs/nighthawkcoders/projects/9?pane=issue&itemId=55135170),  it will contain the tree elements of the assignment (Seed, Player Change, Debugging) in one issues. Triangle Scoring (Best if you review both of the others) Seed (Individual) 90% total, there are 3 significant items items .25 each, prep is another .15. Player changes 90%.   Basic movements of left, right are .8.   Then some other movement is .1. Debug Blogging use rubric on canvas score.
author: Trevor Vick
type: ccc
courses: { csse: {week: 22}, csp: {week: 22 }, csa: {week: 22}}
---

## Seed

Style changes!

### 1. Custom Home Page Buttons

```js
<div class="container">
    <p>
        <em class="blogsDesc">My blogs offer daily accounts of my programming knowledge, along with discoveries and projects I have been pursuing.</em>
    </p>
    <p>
        <a class="blogsLink" href="{{site.baseurl}}/blogs">Blogs</a>
    </p>
    <p>
        <em class="blogsDesc">Find all CSSE-related information on this page. Incldes: Dates, blog type, and other useful information.</em>
    </p>
    <p>
        <a class="blogsLink" href="{{site.baseurl}}/navigation/csse">CSSE</a>
    </p>
    <p>
        <em class="blogsDesc">My game takes inspiration from 2D platformer games such as Mario. Game may not function as expected as it is under development.</em>
    </p>
    <p>
        <a class="gameLink" href="{{site.baseurl}}/game">Game</a>
    </p>
</div>
```
This is the setup (HTML) I used to organize my home page buttons. They provide links to the game, the CSSE tab, and the Blogs page.

```css
    .blogsDesc {
        font-style: normal;
        color: white;
        font-size: 1.625rem;
        font-weight: 400;
        letter-spacing: -1px;
        margin-bottom: 0;
        float: left;
        padding-bottom: 4%;
    }
    .blogsLink {
        display: inline-block;
        padding: 1rem 6rem 1rem;
        margin-bottom: 4%;
        background: rgb(136,235,255);
        background: linear-gradient(90deg, rgba(136,235,255,1) 0%, rgba(91,192,212,1) 100%);
        border: 0;
        font-size: large;
        font-weight:bolder;
        font-weight: 700;
        border-radius: 0.3rem;
    }
    .blogsLink:hover {
        display: inline-block;
        padding: 1rem 6rem 1rem;
        margin-bottom: 4%;
        background: rgb(95,228,255);
        background: linear-gradient(90deg, rgba(95,228,255,1) 0%, rgba(59,189,215,1) 100%);
        border: 0;
        text-decoration: none;
        font-size: large;
        font-weight:bolder;
        font-weight: 700;
        border-radius: 0.3rem;
    }
```

This is the style I used on the buttons. Each button has a gradient color and rounded corners. When you hover over the button, it will darken the background. Although I call them buttons, they are actually a tags (as you may see in the HTML above).

### 2. Other Organization

On top of the home page buttons, I also changed a few style apsects on the home page and game page. First, on the game page, I removed the inverted filter on the canvas to make it a bit easier to look at. Additionally, I removed some of the previous parts of the page that were replaced by the buttons.

## Player Changes

New control system (based off of the reliability of our last game's movement system)

###     1. Movement: Left & right

```js
        if (currentKeys.includes("left") && lopez.isMoving && lopez.x > 0 && !isLoading) {
            lopez.x -= LOPEZ_SPEED
        }
        if (currentKeys.includes("right") && lopez.isMoving && lopez.x < gameFrame.width-(backgroundImage.playerScaleFactor*SPRITE_WIDTH) && !isLoading) {
            lopez.x += LOPEZ_SPEED
        }

        if (lopez.isMoving && currentKeys[currentKeys.length-1] != "up" && currentKeys[currentKeys.length-1] != "down") {
            lopez.currentDirection = currentKeys[currentKeys.length-1];
        }

        ctx.clearRect(0, 0, gameFrame.width, gameFrame.height);

        // Draws Background
        backgroundImage.draw(ctx)
        // Draws the current frame of the sprite.
        if (!isLoading) {
            lopez.draw(ctx);
        }

        setTimeout(() => {requestAnimationFrame(moveLopez);}, LOPEZ_SPEED)
    }
```

This snippet of code makes use the Lopez class (main sprite) and runs each iteration of the game loop. Every iteration, it will check currentKeys (an array of the keys that are active). If the currentKeys array contains a specific direction (left for example), it will change the lopez class accordingly by the speed of the sprite (lopez.x -= LOPEZ_SPEED).

### 2. Movement: Jumping

```js
function moveLopez () {
        lopez.isFloored = lopez.y >= gameFrame.height-(backgroundImage.playerScaleFactor*SPRITE_HEIGHT)
        if (currentKeys.includes("up") && lopez.isMoving && lopez.y > 0 && !isLoading && lopez.isFloored && !lopez.isJumping) {
            lopez.isJumping = true
            lopez.startJumpY = lopez.y
        }
        if (currentKeys.includes("up") && lopez.isMoving && lopez.y > 0 && !isLoading && lopez.isJumping && lopez.currJumpHeight < MAX_JUMP_HEIGHT) {
            lopez.currJumpHeight += 18
            console.log('upper')
        }
        if (lopez.isJumping) {
            if (lopez.y > lopez.startJumpY-lopez.currJumpHeight) {
                lopez.y -= JUMP_POWER
            }
            if (lopez.y <= lopez.startJumpY-lopez.currJumpHeight) {
                lopez.isJumping = false
                lopez.currJumpHeight = MIN_JUMP_HEIGHT
                lopez.startJumpY = undefined;
            }
        }

        if (lopez.isMoving && currentKeys[currentKeys.length-1] != "up" && currentKeys[currentKeys.length-1] != "down") {
            lopez.currentDirection = currentKeys[currentKeys.length-1];
        }

        ctx.clearRect(0, 0, gameFrame.width, gameFrame.height);

        // Draws Background
        backgroundImage.draw(ctx)
        // Draws the current frame of the sprite.
        if (!isLoading) {
            lopez.draw(ctx);
        }

        setTimeout(() => {requestAnimationFrame(moveLopez);}, LOPEZ_SPEED)
    }
```

This snippet has elements of code that give the sprite the ability to jump. It uses the lopez.isJumping property, lopez.isFloored property, lopez.startJumpY property, and lopez.currJumpHeight. It first will check if lopez is on the floor to be able to jump. The longer the user has the jump button held down, the higher he will jump. When the sprite lands, lopez.isJumping is set to false, and lopez.currJumpHeight is reset.

## Debugging

### 1. Debugging in my game

While working on the movement controls for the platformer game, I came in to various errors and issues. To tackle these situations and debug, I used inspect element to use the chrome debugger. This can also be accessed by pressing f12 on the keyboard!

I found that pausing my game with the debugger was very useful in seeing the current state of the code. I could see the current properties of the sprite, and use these values to help me debug my code. I noticed that the debugging process contains some very crucial steps.

#### 1. Check code syntax

Make sure you check the console for any syntax errors in the code.

#### 2. Use console.log

Console.log is a very useful tool in debugging. It can help us see the values of variables while the code is running.

#### 3. Using Googles debugging tool

Googles debugging tool gave me current information of the state of the game and the current properties of the sprite.
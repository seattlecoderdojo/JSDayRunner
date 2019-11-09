# Seattle CoderDojo JavaScript Day Endless Runner
An adaptation of [Emanuele Feronato's]( https://www.emanueleferonato.com/ ) [Phaser Endless Runner tutorial]( https://www.emanueleferonato.com/2018/11/13/build-a-html5-endless-runner-with-phaser-in-a-few-lines-of-code-using-arcade-physics-and-featuring-object-pooling/ ) into a classroom workshop. This is meant to be worked on by middle school or high school students with some understanding of JavaScript *and* with more experienced developers in the room to help them when they get stuck.

Thanks to [Pixabay](https://pixabay.com) for the beginning graphics. Thanks to [Game Art 2D]( https://www.gameart2d.com/freebies.html ) for the dog and cat graphics. Thanks to [Open Game Art & DontMind8]( https://opengameart.org/content/coin-animation ) for the coin.

## Welcome to Funversant Games, new game devs

Welcome to Funversant Games, thanks for joining our coding team. 

You will be working on a new Endless Runner we're developing. Our senior dev on the project got a prototype done, but they've gone off on a six month sabbatical to study underwater basket weaving with the Scuba Monks in Key West.

So let's get you set up with your programming environment and get their prototype cloned into your working directories.

Please go to: [ https://glitch.com/~creative-emmental ]( https://glitch.com/~creative-emmental ) 

Underneath the game preview, please click "remix this."

## Now that you have your dev copy...

The remix has set up your development server with a copy of the current code and assets. Let's click on the sunglasses icon next to the word "Show" at the top of the screen and you can play the prototype. Open it in a new window so you get the full experience.

It's designed for a mobile first experience, which means it's a tap game. You can click on the game to make the runner jump. A fun extra feature is that the runner can double jump, which is jumping again in the middle of a jump.

Let's play it for a few minutes so you can get a feel for it.

## Something to think about

What's actually moving in the game and how does it move?

## What does it need to be better / more fun?

Okay, what does it need? What are some of the ways you think it could be better?

Let's write down a few ideas on the whiteboard as we brainstorm.

## How it works

So we're using a game library called Phaser 3. [ https://phaser.io/phaser3 ]( https://phaser.io/phaser3 )

We're loading the library into the page with a tag in the HTML, then we load your file: script.js.

Let's walk quickly through that code...

**Lines 8-15**: Just some basic game configuration values. The developer was good to use descriptive variable names. I'd really suggest looking here to make some early small tweaks. 

**Lines 18-36**, **Lines 162-175**: Set up the primary game canvas and handle resizing it to fit the window, including when the window changes size.

**Lines 39-161**: This has your main game logic. The logic is split up into five main sections:

### The Game Logic Sections

**Lines 43-52**: The "preload" stage. This loads in all your images, sounds, and other assets that need to be ready for use when the game starts. If you're going to add in pieces, you'll probably need to do so here.

**Lines 53-89**: The "create" stage. This is where we're setting up a lot of the basic scaffolding. 

- Lines 55-60 create a platform "group" of sprites. The platforms are what our hero is running and jumping on. To make it easy to add and remove them, have them all share some properties (and the same graphic), a pool of platform sprite objects is created.
- Line 70 is literally just setting up the jump counter for the number of jumps the player has had in a row.
- Lines 73 - 80 add the first platform to the screen and add the player to the screen. What's interesting here is that instead of just using `this.add.sprite`, it uses `this.physics.add.sprite`, giving the physics engine control of the sprite.
- Lines 82-85 set the player's gravity (how strongly gravity pulls the player down) and set a "collider" between the player and the objects in the platform group. This is so they bump into each other instead of passing through each other. It's what keeps the player on top of the platform... when it's under the player.
- Last, on 88, there's a function that watches for the pointer down input (downward stroke of a mouse-click or tap on the screen) and invokes the jump function.

**Lines 91-115:** The platform factory. 

- Adds platforms to the game when needed. Inactive platform objects are held in a pool. If there are any available, the game pulls one from the pool, activates it, and puts it in the active platform group. If there aren't, it creates one. 
- Down in the update section, when a platform goes off the screen, it deactivates it, removes it from the group, and it goes in the pool.
- Fun to note, when a platform is added to the screen, it gets started moving with a setVelocityX method, which is also manafed by the physics engine. Instead of having to write code to move the platform in every update cycle, Phaser manages that.

**Lines 118-129:** The Jump controller

- The logic seems to be that if the player is either resting on a platform (this.player.body.touching.down) or their number of current jumps is less than the max, give them a jump boost and add to their number of current jumps. 
- Before the boost is given and the jump is added to the current number, it checks if they're touching down and resets the number of current jumps to 0 if they are.

**Lines 130-161:** The update function

- The update function is basically the game loop and runs every frame to manage *some* of the game elements.

- All of this is frame by frame animation, but Phaser takes care of a lot of things. 

  - For example, because of the arcade physics engine, you can just give the player a little shove in the jump controller instead of writing a mathematical function to graph the arc of their jump and move them along it.

- First thing it does is check if the player's Y position is below the bottom of the game frame. If it is... Game over, start over.

  - Something to note, Phaser's X,Y coordinate system is the same as that used in web pages. That means 0,0 is in the top left corner. Y increases as you go *down* and X increases as you go right.
  - That means, when the player's Y coordinate is *greater than* the game height, the player has fallen off the bottom of the game screen.

- The next part runs through the platforms currently on screen. It calculates how far each one is from the right side of the screen, replacing the `minDistance` value each time it hits one that's closer. 

- It also checks to see if any have moved off the left side of the screen, using `killAndHide` and `remove` methods to disable the platform object and move it back into the pool. 

- When a platform is created, it gets a random "next platform distance" within the values specified in the spawn range set in the Game Options (runs between 100 & 350 pixels). If the minDistance is greater than the last platform's next platform distance, a new platform is spawned and added to the screen.

  

## Couple of extra resources

The developer added some sprite sheets to the assets before they left. I think they were going to add animations. They left some notes that might be helpful.

> cat: 8 frames, 107w x 160h
>
> dog (or is it a fox): 8 frames, 105w x 160h
>
> coin: 6 frames, 85w x 85h

## Stuff you might find helpful

**Phaser Code Samples Library:** [ https://phaser.io/examples/v3 ]( https://phaser.io/examples/v3 )

**Phaser API Docs:** [ https://photonstorm.github.io/phaser3-docs/index.html ]( https://photonstorm.github.io/phaser3-docs/index.html )

## Possible Improvements

Here are a few possible improvements that could relate to the ones we brainstormed. Where possible we pulled some stuff that might help from some notes we found in the developer's desk.

- Adjust jump speed (gravity, power), number of jumps?
- Randomize height of where the platforms are put on the screen
  - I think that's set on line 103
- Animate the runner
  - There's a [code sample where a mummy drops a poop emoji every time its animation cycles]( https://phaser.io/examples/v3/view/animation/animation-repeat-event), but with the sprite sheets and some selective use of that demo code, you should be able to animate the hero... and not make it poop.
- Keep score based on platforms passed.
  - Well, you could add to the score every time you take a platform off the screen. But how would you know what the score is? 
  - This part of the ["Making your first Phaser 3 game" tutorial]( https://phaser.io/tutorials/making-your-first-phaser-3-game/part9) gives some very basic instructions. Maybe you could figure out the best size and font-family for the text.
  - Should the score display also show a high score, because the game restarts so fast when you die?
- Add coins to collect.
  - This is getting complicated. You'd have to spawn coins and set them moving *like the platforms*, but you'd have to detect when the hero collides with a coin, remove it, and add to the score. 
  -  A different section of the ["Making your first Phaser 3 game" tutorial]( https://phaser.io/tutorials/making-your-first-phaser-3-game/part8) might have some clues how to do that.
- Could you make it progressively harder as people get a higher score or have played for a while?



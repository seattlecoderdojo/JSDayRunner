# Seattle CoderDojo JavaScript Day Endless Runner
An adaptation of Emanuele Feronato's Phaser Endless Runner tutorials into a classroom workshop

## Welcome to Funversant Games, new Coders

Welcome to Funversant Games, thanks for joining our coding team.  I'm the President of the company and my name is Bigly Important. My friends call me Bigly. You can call me Mr. Important.

You all will be working on a new Endless Runner we're developing. Our senior dev on the project got a prototype done, but he's gone off on a six month sabbatical to study underwater basket weaving with the Scuba Monks in Key West.

So let's get you all set up with your programming environment and get his prototype cloned into your working directories.

Please go to: [ https://glitch.com/~creative-emmental ]( https://glitch.com/~creative-emmental ) 

Underneath the game preview, please click "remix this."

## Now that you have your dev copy...

The remix has set up your development server with a copy of the current code and assets. Let's click on the sunglasses icon next to the word "Show" at the top of the screen and you can play the prototype. Open it in a new window so you get the full experience.

It's designed for a mobile first experience, which means it's a tap game. You can click on the game to make the runner jump. A fun extra feature is that the runner can double jump, which is jumping in the middle of a jump.

Let's play it for a few minutes so you can get a feel for it.

## What does it need?

Okay, what does it need? What are some of the ways you think it could be better?

Let's write down a few ideas on the whiteboard as we brainstorm.

## How it works

So we're using a game library called Phaser 3. [ https://phaser.io/phaser3 ]( https://phaser.io/phaser3 )

We're loading it in via the HTML page, then we load your file: script.js.

Let's walk quickly through that code...

**Lines 8-15**: Just some basic game configuration values. The developer was good to use descriptive variable names. I'd really suggest looking here to make some early small tweaks. 

**Lines 18-36**, **Lines 162-175**: Set up the primary game canvas nd handle resizing it to fit the window, including when the window changes size.

**Lines 39-161**: This has your main game logic. The logic is split up into three main sections:

### The Game Logic Sections

**Lines 43-52**: The "preload" stage. This loads in all your images, sounds, and other assets that need to be ready for use when the game starts. If you're going to add in pieces, you'll probably need to do so here.

**Lines 53-89**: The "create" stage. This is where we're setting up a lot of the basic scaffolding. 

- Lines 55-60 create a platform "group. " The platforms are what our hero is running and jumping on. To make it easy to add and remove them, have them all share some properties (and the same graphic), a pool of platform objects is created.
- Line 70 is literally just setting up the jump counter for the number of jumps the player has had in a row.
- Lines 73 - 80 add the first platform to the screen and add the player. What's interesting here is that instead of just using `this.add.sprite`, it uses `this.physics.add.sprite`, giving the physics engine control of the sprite.
- Lines 82-85 set the player's gravity (how strongly gravity pulls the player down) and set a "collider" between the player and the objects in the platform group. This is so they bump into each other instead of passing through each other. It's what keeps the player on top of the platform... when it's under the player.
- Last, on 88, We set up a function that watches for the pointer down input (downward stroke of a mouse-click, tap on the screen).



## Stuff you might find helpful

**Phaser Code Samples Library:** [ https://phaser.io/examples/v3 ]( https://phaser.io/examples/v3 )

**Phaser API Docs:** [ https://photonstorm.github.io/phaser3-docs/index.html ]( https://photonstorm.github.io/phaser3-docs/index.html )

  





## Possible Improvements

Adjust jump speed (gravity, power)

Randomize height of the platforms

Animate the runner

Keep score based on platforms passed

Add coins and score based on coins collected

Add a pause and "hit any key" for replay

Make it harder by making it faster


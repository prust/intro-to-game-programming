# Intro to Game Programming on the Web

This is a self-paced introduction to programming that is focused on learning how to create a fun video game using web technologies. There are a ton of game libraries and frameworks to choose from, but I think it's good to start with understanding what the web provides all on its own, before looking at libraries and frameworks that build on it.

## v0.1 Creating a blank canvas and a player sprite

There are a wide variety of things you can put on a web page (buttons, images, text input boxes, etc), but with video game programming, you typically just want a big blank canvas that fills the whole page, so that you can paint to it in custom ways. To create one, start a new text file called `index.html` and put this in it:

```html
<canvas id="canvas"></canvas>
```

HTML typically consists of starting tags and ending tags. Here, the `<canvas>` is the start tag and `</canvas>` is the end tag. The start tag has an ID associated with it, `id="canvas"`, so that we can refer to it in our code.

Next we need to add some script, or code, to the page. This goes in a `<script>` tag, like this:

```html
<canvas id="canvas"></canvas>
<script>

</script>
```

The blank area between the start `<script>` tag and the end `</script>` tag is where we'll put the code for our game.

The first thing we'll want to do is draw a player image, or "sprite", to the canvas. For the sake of simplicity, let's make the player a small blue rectangle.

In order to draw the player on the canvas, first we need to create a variable that represents the canvas. You're probably familiar with variables like `x` in math that represent different numbers. In a similar way, programming uses variables that represent numbers, bits of text and pretty much everything else, including the canvas. We can setup the variable by referencing the canvas by its ID:

```html
<canvas id="canvas"></canvas>
<script>
var canvas = document.getElementById('canvas');
</script>
```

The word `var` means that we're creating a new variable and `canvas` is the name of the variable. The `=` is confusing because it means something different than in math. In programming, `=` means that we are **assigning** or **setting** the variable `canvas` to be equal to the result of `document.getElementById('canvas')`. Finally, we end the line with a semicolon `;`, in a similar way to how you would end a sentence with a period.

You would think that now that we have a variable that represents the canvas, we can draw to it. But in most video game programming you don't draw directly to the canvas, instead, you draw to (or in) a drawing context. This is annoying because it's one more thing to type, but it is useful because it allows you to make adjustments to the context (like moving it or flipping it or zooming it) and those adjustments automatically apply to everything drawn to that context:

```html
<canvas id="canvas"></canvas>
<script>
var canvas = document.getElementById('canvas');
var ctx = canvas.getContext('2d');
</script>
```

Now, we're finally ready to draw our blue player sprite to the canvas:

```html
<canvas id="canvas"></canvas>
<script>
var canvas = document.getElementById('canvas');
var ctx = canvas.getContext('2d');
  
ctx.fillStyle = 'blue';
ctx.fillRect(10, 10, 20, 20);
</script>
```

Notice that I'm abbreviating context as `ctx`. Programmers use abbreviations all the time. This might make things slightly more cryptic, but when you're reading and typing things over and over, you learn to appreciate abbreviations.

`fillStyle` defines the style -- in this case, just a solid blue color. `fillRect()` takes four numbers, called "arguments": `fillRect(x, y, w, h)`. The first two numbers represent the x and y coordinates of the upper-left corner and the second two numbers represent the width and height of the rectangle.

## v0.2 Moving the player with the arrow keys

Let's start by allowing the player to move their sprite left and right with the arrow keys. Javascript uses the codes `37` for the left arrow key and `39` for the right arrow key. Let's define these as new variables, so we don't have to remember them:

```html
<canvas id="canvas"></canvas>
<script>
var canvas = document.getElementById('canvas');
var ctx = canvas.getContext('2d');
  
ctx.fillStyle = 'blue';
ctx.fillRect(10, 10, 20, 20);

var left = 37;
var right = 39;
</script>
```

Next we need to add an event handler for the keydown event (when the player presses the key), and move the rectangle left or right:

```html
<canvas id="canvas"></canvas>
<script>
var canvas = document.getElementById('canvas');
var ctx = canvas.getContext('2d');
  
ctx.fillStyle = 'blue';
ctx.fillRect(10, 10, 20, 20);

var left = 37;
var right = 39;
document.addEventListener('keydown', function(event) {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  if (event.keyCode == left)
    ctx.fillRect(0, 10, 20, 20);
  else if (event.keyCode == right)
    ctx.fillRect(20, 10, 20, 20);
});
</script>
```

There is a lot going on here. `document.addEventListener('keydown')` is a way to listen for (and react to) "keydown" events. The function that it takes is a function that runs every time the player presses a key down. Inside the function we clear out the canvas via `clearRect()` (otherwise the new rectangle would just show up on top of the old one). And finally we check if the `keyCode` is left or right and draw the rectangle in the appropriate place.

Notice the double-equals `==`. In programming the `==` is a check for whether the value on the left equals the value on the right. This is different from the single-equals `=` we saw above that **assigns** or **sets** the value on the right to the variable on the left.

If you try this, you'll notice that the rectangle will only go "one step" to the left and "one step" to the right. It won't continue going left or right because we've hard-coded the coordinates `0, 10` for left and `20, 10` for right. To make things more flexible, we need to create a `player` object with an `x` and `y` property:

```javascript
var canvas = document.getElementById('canvas');
var ctx = canvas.getContext('2d');

var player = {
  x: 10,
  y: 10
};
ctx.fillStyle = 'blue';
ctx.fillRect(player.x, player.y, 20, 20);

var left = 37;
var right = 39;
document.addEventListener('keydown', function(event) {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  if (event.keyCode == left)
    player.x = player.x - 10;
  else if (event.keyCode == right)
    player.x = player.x + 10;

  ctx.fillRect(player.x, player.y, 20, 20);
});
```

Now the player can move repeatedly (even off the screen) left or right. 


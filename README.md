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



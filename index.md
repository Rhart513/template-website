# This is a heading

Replace

``import turtle
import random

# We will need the edges of our box, so we set them
width = 300
height = 400
window = turtle.Screen()
window.setup(width, height)
window.tracer(0)

color = ["blue",
        "yellow",
        "red",
        "darkgreen", 
        "cyan", 
        "violet",
        "magenta",
        "orange",
        "purple", 
        "navy", 
        "brown", 
        "maroon",
        "turquoise", 
        "lightgreen", 
        "green", 
        "skyblue", 
        "black", 
        "gold",
        "gray"]

N = 5 # Number of balls
balls = [] # A list to hold the balls

# Set up N balls and start them in random positions
for i in range(N):
    balls.append(turtle.Turtle())
    balls[i].penup()
    balls[i].shape("turtle")
    balls[i].color(color[i%len(color)])

    # Set random starting position
    balls[i].setx(random.randint(0,height / 4))
    balls[i].sety(random.randint(0,height / 4))

# Free fall acceleration -g
g = -9.81

# Timestep size
t = 0.08

# Starting velocity is now also a list, we need one velocity per ball
ux = []
uy = []
vy = []
sx = []
sy = []
for i in range(N):
    ux.append(0)
    uy.append(0)
    vy.append(0)
    sx.append(0)
    sy.append(0)
ux[0]=6
ux[1] = 5
ux[2] = 3
ux[3] = 6
ux[4] = -3
while True:
    for i in range(N):
        vy[i] = vy[i] + g*t
	sy[i] = vy[i]*t
	sx[i] = ux[i]*t
	balls[i].sety(balls[i].ycor() + sy[i])
	balls[i].setx(balls[i].xcor() + sx[i])  
	if (balls[i].ycor() <= -200) or (balls[i].ycor()>=200):
		vy[i] = -vy[i]
		balls[i].sety(balls[i].ycor() - g*t*t) 
	if (balls[i].xcor() <= -150) or (balls[i].xcor() >= 150):
		ux[i] = -ux[i]
		balls[i].setx(balls[i].xcor() - g*t*t)
    window.update()
``
with your own code below. You can also add text above or below but don't modify the code.


<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js" type="text/javascript"></script> 
<script src="https://cdn.jsdelivr.net/npm/skulpt@1.2.0/dist/skulpt.min.js" type="text/javascript"></script> 
<script src="https://cdn.jsdelivr.net/npm/skulpt@1.2.0/dist/skulpt-stdlib.js" type="text/javascript"></script> 

<script type="text/javascript"> 
function outf(text) { 
    var mypre = document.getElementById("output"); 
    mypre.innerHTML = mypre.innerHTML + text; 
} 
function builtinRead(x) {
    if (Sk.builtinFiles === undefined || Sk.builtinFiles["files"][x] === undefined)
            throw "File not found: '" + x + "'";
    return Sk.builtinFiles["files"][x];
}

function runit() { 
   var prog = document.getElementById("yourcode").value; 
   var mypre = document.getElementById("output"); 
   mypre.innerHTML = ''; 
   Sk.pre = "output";
   Sk.configure({output:outf, read:builtinRead}); 
   (Sk.TurtleGraphics || (Sk.TurtleGraphics = {})).target = 'mycanvas';
   var myPromise = Sk.misceval.asyncToPromise(function() {
       return Sk.importMainWithBody("<stdin>", false, prog, true);
   });
   myPromise.then(function(mod) {
       console.log('success');
   },
       function(err) {
       console.log(err.toString());
   });
} 
</script> 

<h3>Try This</h3> 
<form> 
<textarea id="yourcode" cols="40" rows="10">
import turtle

t = turtle.Turtle()
t.forward(100)

</textarea><br /> 
<button type="button" onclick="runit()">Run</button> 
</form> 
<pre id="output" ></pre> 
<!-- If you want turtle graphics include a canvas -->
<div id="mycanvas"></div> 

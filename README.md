# Blooming Fireworks 
Chang Wang 20036997

[[MIMIC]](https://mimicproject.com/code/fe387a7c-fb42-fde2-ea05-cba3733b90fd)

[[BLOG]](https://changw1006.wixsite.com/mysite/post/term1-coding1-final-project)  

![](https://static.wixstatic.com/media/27541e_07cd6faf49f547eb87895d84424be60e~mv2.png/v1/fill/w_828,h_688,al_c,q_90,usm_0.66_1.00_0.01/27541e_07cd6faf49f547eb87895d84424be60e~mv2.webp)

## **Source of inspiration**
The Chinese New Year is approaching again. In the previous Spring Festival, the family gathered for dinner, watched the Spring Festival Gala together, chatted, and set off fireworks. However, due to environmental protection and security issues, China has banned fireworks in recent years. I miss the Spring Festival with fireworks, so this project I did is about BloomingFireworks. My purpose is to restore the Spring Festival fireworks in my childhood memories.

![](https://static.wixstatic.com/media/27541e_db3450877d7a4555817b9851dc0cdc40~mv2.jpg/v1/fill/w_864,h_576,al_c,lg_1,q_90/27541e_db3450877d7a4555817b9851dc0cdc40~mv2.webp)

## **Sketch**
![](https://static.wixstatic.com/media/27541e_4bfb385159644597866cd944a537cbf4~mv2.png/v1/fill/w_470,h_458,al_c,q_90,usm_0.66_1.00_0.01/27541e_4bfb385159644597866cd944a537cbf4~mv2.webp)



## **STEPS**
### Step1
First we need to set up some basic design such as background color in `<style></style>` using css language, and set up a `<canvas>`. 

````<style>
body {
  background: #000427;
  overflow: hidden; 
}

canvas {
  height: 100%;
  left: 0;
  position: absolute;
  top: 0;
  width: 100%;
}</style>
````

### Step2
Then set the variables will to be applied
````<script>
'use strict';

function _classCallCheck(instance, Constructor) { if (!(instance instanceof Constructor)) { throw new TypeError("Cannot call a class as a function"); } }

var Scene = function () {
  function Scene() {
    var _this = this;

    _classCallCheck(this, Scene);

    this.PI = Math.PI;
    this.TAU = this.PI * 2;
    this.GOLDEN = (Math.sqrt(6) + 1) / 2;
    this.canvas = document.querySelector('canvas');
    this.ctx = this.canvas.getContext('2d');
    this.dpr = window.devicePixelRatio;
    this.reset();
    window.addEventListener('resize', function () {
      return _this.reset();
    });
    this.loop();
  }
````
In `<script></script>` using functions such as Constructor to create dynamic effects in the following. 
this.TAU is the distance between each "branch" of the fireworks, and this.GOLDEN is the rate of color change.

### Step3
Write function to execute drawing 2D Graphics.
````
Scene.prototype.reset = function reset() {
    this.width = window.innerWidth;
    this.height = window.innerHeight;
    this.hwidth = this.width * 0.5;
    this.hheight = this.height * 0.5;
    this.canvas.width = this.width * this.dpr;
    this.canvas.height = this.height * this.dpr;
    this.ctx.scale(this.dpr, this.dpr);
    this.ctx.translate(~ ~this.hwidth, ~ ~this.hheight);
    this.ctx.globalCompositeOperation = 'lighter';
    this.tick = 320;
  };
    Scene.prototype.loop = function loop() {
    var _this2 = this;
````
In Scene.prototype, I designed the position of the dynamic pattern on the canvas. After calculation, I placed the pattern in the middle of the canvas, and use the loop function.

### Step4
Then set up various effects of fireworks.
````
Scene.prototype.loop = function loop() {
    var _this2 = this;

    requestAnimationFrame(function () {
      return _this2.loop();
    });
    this.tick++;
    this.ctx.clearRect(-this.hwidth, -this.hheight, this.width, this.height);
    var count = 150;
    var angle = this.tick * -0.001;
    var amp = 0;
    for (var i = 2; i < count; i++) {
      angle += this.GOLDEN * this.TAU + Math.sin(this.tick * 0.03) * 0.001;
      amp += (i - count / 2) * 0.01 + Math.cos(this.tick * 0.015) * 1;
      var x = Math.cos(angle) * amp + Math.cos(this.tick * 0.0075) * (count - i) * 0.3;
      var y = Math.sin(angle) * amp + Math.sin(this.tick * 0.0075) * (count - i) * 0.3;
````
This part of the requestAnimationFrame function is the focus.

I set count, angle, and amp variables respectively. 
Use Math.sin() to calculate the rotation angle of the tick. 
Use Math.cos() to calculate the size, distance and speed of each firework bloom.
The variables x and y are also calculated using Math.sin() and Math.cos() respectively.

### Step5
The variables radius, scale, hue, saturation, lightness, and alpha have also been calculated to my satisfaction.
````
var radius = 0.1 + i * 0.02;
      var scale = 0.1 + amp * 0.1;
      var hue = this.tick + angle / this.TAU * 0.4 + 60;
      var saturation = 90;
      var lightness = 60;
      var alpha = 0.7 + Math.cos(this.tick * 0.03 + i) * 0.3;
````


### Step6
Next are some adjustments to the firework style.
````
this.ctx.save();
      this.ctx.translate(x, y);
      this.ctx.rotate(angle);
      this.ctx.scale(scale, 1);
      this.ctx.rotate(this.PI * 0.3);
      this.ctx.fillStyle = 'hsla(' + hue + ', ' + saturation + '%, ' + lightness + '%, ' + alpha + ')';
      this.ctx.fillRect(-radius, -radius, radius * 2, radius * 2);
      this.ctx.restore();

      this.ctx.beginPath();
      this.ctx.arc(x, y, radius * 12, 0, this.TAU);
      this.ctx.fillStyle = 'hsla(' + hue + ', ' + saturation + '%, ' + lightness + '%, ' + alpha * 0.05 + ')';
      this.ctx.fill();
    }
  };

  return Scene;
}();
````
When the effect is over, return to Scene and loop the demonstration.

## **JavaScript language & notes**
`Math.sin(x)` returns the sine (a value between -1 and 1) of the angle x (given in radians).
If you want to use degrees instead of radians, you have to convert degrees to radians:
Angle in radians = Angle in degrees x PI / 180.

`Math.cos(x)` returns the cosine (a value between -1 and 1) of the angle x (given in radians).
If you want to use degrees instead of radians, you have to convert degrees to radians:
Angle in radians = Angle in degrees x PI / 180.


## **HTML5 language & notes**
Almost all of this project uses the function of canvas.
Record the order in which you want to make a effect like this in the canvas:
1. Define the graphic style
radius 
scale 
hue 
saturation
lightness
alpha

2. Movement sequence
save
translate
rotate
scale
rotate
fill Style
fill Rect
restore
begin Path
arc
 



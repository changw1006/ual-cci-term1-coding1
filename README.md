# Blooming Fireworks 
Chang Wang 20036997

**Link to the project** : https://mimicproject.com/code/fe387a7c-fb42-fde2-ea05-cba3733b90fd

## Source of inspiration
The Chinese New Year is approaching again. In the previous Spring Festival, the family gathered for dinner, watched the Spring Festival Gala together, chatted, and set off fireworks. However, due to environmental protection and security issues, China has banned fireworks in recent years. I miss the Spring Festival with fireworks, so this project I did is about BloomingFireworks. My purpose is to restore the Spring Festival fireworks in my childhood memories.

## Project description
In <style></style> using css language, I did some basic design such as background color.

In <script></script> using functions such as Constructor to create dynamic effects in the following <script></script>.

this.TAU is the distance between each "branch" of the fireworks, and this.GOLDEN is the rate of color change.

In Scene.prototype, I designed the position of the dynamic pattern on the canvas. After calculation, I placed the pattern in the middle of the canvas.

The part of the requestAnimationFrame function is the focus.

I set count, angle, and amp variables respectively. 
Use Math.sin() to calculate the rotation angle of the tick. 
Use Math.cos() to calculate the size, distance and speed of each firework bloom.
The variables x and y are also calculated using Math.sin() and Math.cos() respectively.

The variables radius, scale, hue, saturation, lightness, and alpha have also been calculated to my satisfaction. 
Next are some adjustments to the firework style.

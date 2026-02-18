<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>3 Ways to Create Angled Edges With SVG</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>In this tutorial you’ll learn three ways to create easy angled edges using SVG. To begin with 
we’ll use an <b>inline SVG</b>, then we’ll use an <b>SVG background</b> on a pseudo-element, before 
finishing off with a <b>Sass mixin</b>. Let’s dive in!</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3>1. Inline SVG</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Let’s start with an SVG, within a container, in our markup:</p>

```
<div class="hero">
  <svg viewBox="0 0 100 100" preserveAspectRatio="none">
        
  </svg>
</div>
```

<p>We’ll come back to the details of what we’ve done in a moment. Now add some basic styles to give 
our hero some dimensions and a gradient background:</p>

```
body {
  background-color: #eaeaea;   
}
.hero {
  position: relative;
  height: 300px;
  background-image: linear-gradient(#4568dc, #b06ab3);
}
```

<p>That gives us the following:</p>
<a href="https://codepen.io/tutsplus/pen/oMwqQq">Codepen.io</a>

<p>But let’s imagine we want to have that bottom edge as an angle going up towards the right. 
We’re going to do that with our SVG. In it, we’re going to create a polygon with some point 
coordinates:</p>

```
<div class="hero">
  <svg viewBox="0 0 100 100" preserveAspectRatio="none">
    <polygon points="0,100 100,0 100,100" />
  </svg>
</div>
```

<p>You’ll now see a large, black triangle in the bottom right of your page. Through our CSS we can 
style that triangle to suit our needs, filling it the same as our background so the hero appears 
to have been sliced at the bottom:</p>

```
svg {
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 10vw;
  fill: #eaeaea;
}
```

<p>That gives us:</p>

<a href="https://codepen.io/tutsplus/pen/rrwdgm">Codepen.io</a>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3>2. Pseudo-Element + SVG</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3>2. SVG background</h3

<p>Our second approach improves on the first, in that content within the gray area won’t be cut off 
by overlaying a gray triangle. We’ll being again with a simple container div:</p>

```
<div class="hero">    
</div>
```

<p>This time we’ll control the masking all from within our CSS, starting with the hero styles we 
used in the last demo:</p>

```
body {
  background-color: #eaeaea;   
}
.hero {
  position: relative;
  height: 300px;
  background-image: linear-gradient(#4568dc, #b06ab3);
}
```

<p>Now we’ll add a pseudo-element to our hero, to which we’ll add the SVG as a background image. 
First, we’ll need to encode our SVG so that we can actually use it in CSS. So grab the SVG code we 
wrote last time, change the points to 0,0 100,0 0,100 in order to flip it round, head over to 
<a href="https://yoksel.github.io/url-encoder/">URL-encoder for SVG</a>, and paste the contents 
into the box:</p>

<a href="https://yoksel.github.io/url-encoder/">SVG encoder</a>

<p>Copy the <b>Ready for CSS</b> snippet and paste it into the pseudo-element styles:</p>

```
.hero::after {
  background-image: url("data:image/svg+xml, %3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'
  preserveAspectRatio='none'%3E%3Cpolygon points='0,0 100,0 0,100' /%3E%3C/svg%3E");
}
```

<p>You can also add a fill='' attribute if you like, after the viewBox attribute for example. Add 
some more properties to position and size the pseudo-element:</p>

```
.hero::after {
  background-image: url("data:image/svg+xml, %3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100' fill='tomato' preserveAspectRatio='none'%3E%3Cpolygon points='0,0 100,0 0,100' /%3E%3C/svg%3E");   
  background-position: center center;
  background-repeat: no-repeat;
  background-size: 100% 100%;
  content: '';
  height: 10vw;
  width: 100%;
  position: absolute;
  bottom: -10vw;
}
```

<p>That gives us this:</p>

<a href="https://codepen.io/tutsplus/pen/yqXjrv">Codepen.io</a>

<p>Thanks to our Ziggy Stardust colors we can clearly see our SVG like this. Now we just need to color 
the triangle (using the <b>fill=''</b> attribute) so that it’s the same color as the purple at the bottom 
of the gradient:</p>

<a href="https://codepen.io/tutsplus/pen/mjwKVE">Next Codepen.io</a>

<p>Note: thanks to Bob Proctor for pointing out that hex values in the fill attribute don’t seem to 
be recognised by FireFox. You’ll need to use RGB, or HSL, or name values.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h4>The Importance of VW Units</h4>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>There’s a reason we used vw units for the height of our SVG: we want the angle of our triangle 
to remain consistent no matter what the width of the viewport. If we were to use px units, the height 
of the triangle wouldn’t change for narrower screens, which would make the angle of the triangle 
more acute. Try it yourself!</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3>3. SASS mixin</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>This final approach uses a Sass mixin to do all the heavy lifting, but it essentially achieves 
what we did in the previous example. Head over to the Angled Edges GitHub repo, grab the mixin, and 
include it in your project (I’m going to paste the whole thing into the SCSS window of a CodePen 
project).</p>

<p>Next, add our old friend the hero div to your markup. Add the basic styles too, so that we get 
the usual 300px gradient effect.</p>

<p>Then, within our .hero we add the mixin:</p>

```
@include angled-edge();
```

<p>The parameters we need are as follows: we need our triangle to be outside the hero, at the bottom. 
The position of the point where the angle begins is lower right, the color we’re after is the purple 
'#b06ab3', and then the height of the triangle will be 100. The limitation of this is that the mixin 
doesn’t accept relative values for the height or the width.</p>

<p>Our mixin looks like this:</p>

```
@include angled-edge("outside bottom", "lower right", #b06ab3, 100);
```

<p>And this is what we get:</p>

<a href="https://codepen.io/tutsplus/pen/wxeXjy">Codepen.io</a>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3>Conclusion</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>So there we have it; three methods for achieving angled edges. Each one has its merits, and practicing 
each one will give you a solid understanding of how SVGs can be manipulated for visual effect.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3>More SVG, Gradients, and Angles in Web Design</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p><a href="https://webdesign.tutsplus.com/tutorials/how-to-create-a-loader-icon-with-svg-animations--cms-31542">
How to create a loader icon with SVG animation</a></p>

<p><a href="https://webdesign.tutsplus.com/tutorials/how-to-use-gradients-on-the-web--cms-29922">
How to CSS gradients on the web</a></p>

<p><a href="https://webdesign.tutsplus.com/tutorials/how-to-create-a-split-screen-slider-with-javascript--cms-28844">
How to create a split screen slider with JavaScript</a></p>



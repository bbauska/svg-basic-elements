<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>Basic SVG Elements</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>You can get into a lot of complexity with SVG, but that’s not necessary for the icons we’ll be 
making. The following list covers the building blocks we’ll need.</p>

<ul>
  <li><b>&lt;svg&gt;</b> Wraps and defines the entire graphic. <b>&lt;svg&gt;</b> is to a scalable 
    vector graphic what the <b>&lt;html&gt;</b> element is to a web page.</li>
  <li><b>&lt;line&gt;</b> Makes single straight lines.</li>
  <li><b>&lt;polyline&gt;</b> Makes multi-segment lines.</li>
  <li><b>&lt;rect&gt;</b> Makes rectangles and squares.</li>
  <li><b>&lt;ellipse&gt;</b> Makes circles and ovals.</li>
  <li><b>&lt;polygon&gt;</b> Makes straight sided shapes, with three sides or more.</li>
  <li><b>&lt;path&gt;</b> Makes any shape you like by defining points and the lines between them.</li>
  <li><b>&lt;defs&gt;</b> Defines reusable assets. Nothing placed inside this <b>&lt;defs&gt;</b> 
    section is visible initially. <b>&lt;defs&gt;</b> is to a scalable vector graphic what the 
	<b>&lt;head&gt;</b> element is to a web page.</li>
  <li><b>&lt;g&gt;</b> Wraps multiple shapes into a group. Place groups in the &lt;defs&gt; section 
    to enable them to be reused.</li>
  <li><b>&lt;symbol&gt;</b> Like a group, but with some extra features. Typically placed in the 
    <b>&lt;defs&gt;</b> section.</li>
  <li><b>&lt;use&gt;</b> Takes assets defined in the <b>&lt;defs&gt;</b> section and makes them 
    visible in the SVG.</li>
</ul>

<p>As we go through and create our icons, we’ll be working through this list of elements in the 
order seen above.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3>Starter Files</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Before we get started, grab yourself a copy of 
<a href="https://github.com/tutsplus/how-to-hand-code-svg">the starter files from the GitHub repo</a>. 
You can either download a .zip file, or clone the repo to your own system.</p>

<p>We’re going to begin with a document that has some basic HTML and CSS already in place. This will 
give some styling to the SVGs we’ll be making, and will also set you up with a little grid on the 
page. We’ll be creating our icons over the top of this grid, and hopefully it will help you visualize 
the coordinates you’re working with when laying down your SVGs.</p>

<p>When you open up “handcodedsvg.html” from the source “Starter Files” folder you should see the 
following:</p>

<svg-image-1.png>

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3>Quick Primer on x and y Values</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>When working in 2D space on a website, the horizontal axis is represented by x and the vertical 
axis is represented by y. Positions along each of these axes are represented by numbers. If we want 
to move something to the right, we’ll need to use increasing x values, and to move to the left we’ll 
use decreasing x values. Likewise, to move something down we’ll use increasing y values, and to move 
something up we’ll use decreasing y values.</p>

<p>A common shorthand for expressing the x and y values of a single point is (x, y). For example, a 
point at 10 on the x axis and 50 on the y axis might be written as (10, 50). I’ll use this shorthand 
from time to time in this tutorial.</p>

<p>Notice the two darkest lines on our grid? We’re going to place our SVG so its top left corner aligns 
with the place they intersect. As such, that intersection point will represent the position x = 0 and 
y = 0 , or (0,0), in our SVG.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3>The Background Grid</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Each of the lightest grid lines represents 10px, and the medium thickness lines represent 100px. 
So if we wanted to move an object down from one medium thickness line to the next, we’d increase 
its location on the y axis by one 100px.</p>

<p>If that still sounds a little unclear, don’t worry this will all make sense as we get into the 
practicalities of creating our SVG icons.</p>

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3>Default SVG Styling</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Note that in the starter HTML file there is some included CSS with default styling for our soon-to-be-created SVG icons:</p>

```
svg {
  stroke: #000;
  stroke-width: 5;
  stroke-linecap: round;
  stroke-linejoin: round;
  fill: none;
}
```

<p>This will set our icons to have no fills, and black 5px wide strokes with rounded caps and joins.</p>


<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>1. Setup the SVG</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>The first step in creating any SVG is to lay down an <b>&lt;svg&gt;&lt;/svg&gt;</b> element. 
Anything you want your SVG to display will have to be between these tags. There are a few attributes 
you can use on this element, but we’ll keep things simple and just use width and height.</p>

<p>Add the following code in the <b>&lt;body&gt;</b> section of your HTML document:</p>

```
<svg width="750" height="500">
</svg>
```

<blockquote>
The CSS in our starter file is going to offset this SVG down and to the right by 100px so its top 
left corner will be positioned at the intersection point of the two darkest lines on our background 
grid. And the values in the CodePen demos throughout this tutorial may differ slightly too–but feel 
free to play around with them.
</blockquote>

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>2. Create “Left Align” Icon</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Let’s start by using the <b>&lt;line&gt;</b> element to create this left align icon:</p>

<!-- svg-image-2.png -->

<p>The line element has four attributes you’ll need to use:</p>

<ul>
  <li><b>x1</b> horizontal starting point of the line</li>
  <li><b>y1</b> vertical starting point of the line</li>
  <li><b>x2</b> horizontal ending point of the line</li>
  <li><b>y2</b> vertical ending point of the line</li>
</ul>

<p>To summarize the above, you use the <b>x1</b> and <b>y1</b> attributes to set where the line 
begins, and the 
<b>x2</b> and <b>y2</b> attributes to set where the line ends.</p>

<p>Let’s create the first line of our icon, the one at the top. We’re going to make the line <b>45px</b> 
long, however the <b>5px</b> stroke we’re using is going to add some extra pixels around the outside of 
our line. As such we’ll need to offset our line down and to the right by <b>3px</b> to ensure none of 
the extra pixels created by the stroke are clipped off.</p>

<p>For that reason, we’re going to start our line at a position of <b>3</b> on the <b>x</b> axis 
and <b>3</b> on the <b>y</b> axis. We can set this line starting point of <b>(3,3)</b> by using 
the attributes <b>x1="3" y1="3"</b>.</p>

<p>We want the line to be <b>45px</b> long, so we’re going to add <b>45</b> to our starting <b>x</b> 
position of <b>3</b>, giving us <b>48</b> as the value we want to set for <b>x2</b>. We want the line 
to finish at the same position on the horizontal axis, so we’ll set <b>y2</b> to equal <b>3</b>, i.e. 
the same value we gave to <b>y1</b>. We’ll add this <b>(48,3)</b> line ending point via the attributes 
<b>x2="48" y2="3"</b>.</p>

```
<line x1="3" y1="3" x2="48" y2="3"></line>
```

<p>Check your browser preview and you should see a <b>45px</b> long black line with nice rounded caps.</p>

<p>Now we can go ahead and add the next three lines to our icon. We want to end up with four lines in total. 
The first and third should be <b>45px</b> long, and the second and fourth should be <b>62px</b> long. We 
also want a vertical gap between each of <b>16px</b>.

<p>We can achieve this with the following code:</p>

```
<line x1="3" y1="3" x2="48" y2="3"></line>
<line x1="3" y1="19" x2="65" y2="19"></line>
<line x1="3" y1="35" x2="48" y2="35"></line>
<line x1="3" y1="51" x2="65" y2="51"></line>
```

<p>The <b>y</b> values of each line incrementally increase by <b>16px</b> in order to create the 
required vertical gap.</p>

<p>Take another look at your browser preview and you should see all four lines. You can also edit 
the SVG directly in this pen:</p>

<p><a href="https://codepen.io/tutsplus/pen/GQpJNL">CodePen.io example</a>.</p>

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3>Comment Out Your Icons As We Go</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>With that code in place, your first icon is already made. We’re ready to move onto creating the 
next icon, and we’re going to want to make it in the same position on the grid, but right now the 
left align icon is in the way. As such, for now just comment out its code to clear the space. We’re 
going to come back and uncomment it later when we turn our icons into reusable assets.</p>

<p>You’ll need to do the same thing for each icon as we go, commenting it out after you finish creating 
it. For that reason it’s probably also a good idea to add a little note above the code for each icon so 
you know which is which when you come back to them later.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>3. Create a “Right Caret” Icon</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>For this icon, let’s use the next evolution of the <b>&lt;line&gt;</b> element: the <b>&lt;polyline&gt;</b>. 
We’ll be using it to create a right pointing caret.</p>

<p>The <b>&lt;polyline&gt;</b> element only has one attribute: <b>points</b>. In here you use pairs of numbers 
to set a series of <b>points</b>. Lines will automatically be drawn between them. The number pairs are simply 
written one number after the other inside the points attribute. Comma separation is not required, though 
it can optionally be included. For readability you might also like to put each pair of values on its own 
line in your code.</p>

<p>We’re going to start our right caret’s polyline at the same spot we started our last icon, that being <b>(3,3)</b> 
to ensure our stroke and caps don’t get clipped. We want our second point to move over to the right, and down by 
<b>25px</b>, so we’ll set it to <b>(30,28)</b>. Our third point should be vertically aligned with the first point, 
and move down by another <b>25px</b>, so it will be set to <b>(3,53)</b>.</p>

<p>We can add these points into our polyline’s points attribute like so:</p>

```
<polyline points=" 
3 3 
30 28 
3 53 
"></polyline>
```

<p>If you want more concise code, you could also write the above as:</p>

```
<polyline points="3 3, 30 28, 3 53"></polyline>
```

or

```
<polyline points="3 3 30 28 3 53"></polyline>
```

<p>Take a look at your browser preview and you should see your right caret icon showing: another 
icon done, just like that!</p>

<p><a href="https://codepen.io/tutsplus/pen/PQPqVq">Codepen.io</a>.</p>

<p>Once again, comment out this icon and give it a little note so you know which one it is before 
moving onto the next icon.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>4. Create a “Browser” Icon</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Now we have lines down pat, let’s create some shapes, starting with a rectangle (&lt;rect&gt;). We’re 
going to use it in conjunction with a couple of <line>s to create a browser icon.</p>

<!-- svg-image-4.png -->

<p>Rectangles and squares can be created with the <rect> element, which has four attributes you’ll 
need to provide:</p>

<ul>
  <li><b>x</b> the top left corner position on the x axis</li>
  <li><b>y</b> the top left corner position on the y axis</li>
  <li><b>width</b> width of the shape</li>
  <li><b>height</b> height of the shape</li>
</ul>

<p>You can also use the attributes rx and ry to create rounded corners if you’d like.</p>

<p>We’re going to create a rectangle with its top left corner offset by 3px in both directions, 
again to avoid clipping the stroke, so we’ll use the attributes x="3" y="3". We want it to be 
80px wide by 60px high, so we’ll also use the attributes width="80" height="60".</p>

<p>As such our full rectangle code should be:</p>

```
<rect x="3" y="3" width="80" height="60"></rect>
```

<p>Save your code and take a look at your browser preview. You should see a neat little rectangle 
sitting there.</p>

<p>Now all we need to do is add a horizontal line across the top, and a vertical line near the top 
left, as you see depicted in the image at the start of this section. We’ll use the same line creation 
process as we did before, and our complete browser icon code should look like this:</p>

```
<rect x="3" y="3" width="80" height="60"></rect>
<line x1="3" y1="19" x2="83" y2="19"></line>
<line x1="20" y1="3" x2="20" y2="17"></line>
```

<p>Take a moment to look at the coordinates provided in the two line attributes, and maybe change 
their values around a little bit so you can see how they’re working in this icon.</p>

<p><a href="https://codepen.io/tutsplus/pen/PQPqMZ">Codepen.io</a>.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>5. Create an “Alert” Icon</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Now that we have rectangles creation under control, let’s try out using <b>&lt;ellipse&gt;</b>s. 
We’re going to use two of them, along with a <line>, to create this alert icon:</p>

<!-- svg-image-5.png -->

<p>Like rectangles, the <ellipse> element also requires four attributes, however they are a little 
different to those of rectangles. Instead of using width and height we set a horizontal and vertical 
radius. And instead of positioning the top left corner of the shape, we position its center:</p>

<ul>
  <li><b>cx</b> the center position on the <b>x</b> axis. Think “cx for center x”.</li>
  <li><b>cy</b> the center position on the <b>y</b> axis. Think “cy for center y”.</li>
  <li><b>rx</b> the size of the radius on the <b>x</b> axis, i.e. the shape’s height divided in 
    half. Think “rx for radius x”.</li>
  <li><b>ry</b> the size of the radius on the <b>y</b> axis, i.e. the shape’s width divided in 
    half. Think “ry for radius y”.</li>
</ul>

<p>We want a perfectly round circle that’s 80px wide by 80px high, which means we need its radius 
to be 40px on both axes. We’ll set this with the attributes rx="40" ry="40".</p>

<p>We also want the circle to sit flush with the darkest lines on our graph. Given that our circle 
will be 80px wide and high, that would place its center point at 40px. We also need to allow for 
our 3px offset to avoid clipping however, so that means our circle’s center point should be a 43px 
on both axis. We’ll set this with the attributes cx="43" cy="43".</p>

<p>Putting all that together, we get this code:</p>

```
<ellipse cx="43" cy="43" rx="40" ry="40"></ellipse>
```

<p>Check your browser preview and you should now see a circle on your page.</p>

<p>We’re going to add a second circle now, to create the dot at the bottom of the exclamation mark. 
We’ll create this in just the same way, the only difference being we’re going to use an inline style 
to set the fill to black:</p>

```
<ellipse style="fill:black;" cx="43" cy="65" rx="5" ry="5"></ellipse>
```

<p>Finally, we just need to add a line to create the other part of the exclamation mark. Once again 
we’re using the same techniques as with the other lines we’ve used so far, with the only difference 
being we’ll use an inline style to thicken this stroke width up from 5px to 8px.</p>

<p>The completed code for our alert icon is as follows:</p>

<a href="https://codepen.io/tutsplus/pen/rJOOaK">Codepen.io</a>

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>6. Create a “Play” Icon</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Now we have the hang of the relatively fixed shapes of rectangles and ellipses, we’re ready to 
roll our own shapes using the <polygon> element. We can create any multi-sided shape we want with 
this, from octagons to stars. However we’ll keep things straight forward for now and create a triangle. 
We’ll combine it with an <ellipse> to create a play icon:</p>

<p>The &lt;polygon&gt; element is almost identical to the <b>&lt;polyline&gt;</b> element. It too has just one 
attribute, points, in which you use pairs of values to set each point that makes up the shape. The 
difference is that while a polyline will remain open, a polygon will automatically close itself.</p>

<p>Let’s start by getting the circle down that our polygon will sit inside of. We’ll use the exact same 
ellipse we did in our alert icon:</p>

```
<ellipse cx="43" cy="43" rx="40" ry="40"></ellipse>
```

<p>Now let’s create our polygon. We’re going to place three points, and lines will automatically
be generated between these points to create a triangle. The points will be (35,23), (60,43) and 
(35,63). As such our polygon’s code will be:</p>

```
<polygon points="35 23, 60 43, 35 63" />
```

<p>And our complete play icon’s code is:</p>

<a href="https://codepen.io/tutsplus/pen/yvYYYv">Codepen.io</a>

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>7. Create a “Download” Icon</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Now we’ll move onto the most potentially complex, but simultaneously most flexible means of producing 
SVG shapes, and that is the <path> element. Creating a path is a little like creating a polygon, 
where you lay out your shape a piece at a time. However with a path you directly create each point 
and line yourself without automation, and you also have the option to create curves between points 
instead of straight lines.</p>

<p>A path can be used to create just about anything, but beyond a certain level of complexity you 
are still better off using a vector design application rather than hand coding. For that reason, 
we’re going to focus on a small subset of path functionality, and use it to create this download icon:</p>

<!-- image -->

<p>Technically, you could create the above shape with a polygon, but this arrow will give us a good way 
to get across how the path element works.</p>

<p>We’ll be using only one of the attributes of <path>, and that is d. The d stands for “data”, and it’s 
in here you’ll define all the points and lines of your path. Within this attribute, commands to set the 
points of a path and create lines between them are provided via single letters such as M or L, followed 
by a set of x and / or y coordinates.</p>

<p>There are several of these commands, but to give you an intro to working with <path> we’ll stick to a few that can be realistically used when hand coding. They are as follows:</p>

<ul>
  <li><b>M</b> Represents moveto. It starts a new path at a given position, defined with x and y values. Imagine this is like hovering your mouse over a point on your canvas, ready to draw. The capital M indicates moving to an absolute set of coordinates. (Lower case m would indicate relative coordinates).</li>
  <li><b>L</b> Represents lineto. Draw a line from the current position to a new position. The capital L indicates moving to an absolute set of coordinates. (Lower case l would indicate relative coordinates).</li>
  <li><b>Z</b> Represents closepath. It converts the path into a closed shape by drawing a straight line between the current point to the first point created in the path.</li>
</ul>

<p>You should definitely view these three commands, (and the icon we’ll create with them), as an 
introductory primer to the <path> element. To really get the most out of it you’ll want to familiarize 
yourself with all the commands at your disposal.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3>Code Your Download Icon</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>To code your download icon path I recommend first adding in the empty path element:</p>

```
<path d=" 

"></path>
```

<p>From here, add in each command one at a time, saving and viewing the progress of the shape so you 
see how it is created. I also recommend putting each command on its own line for readability.</p>

<ol>
  <li>First, we want to move to (18,3), the point at which we want our arrow to begin. To do this 
    we’ll add the command M 18 3 to our path’s d attribute.</li>
  <li>Next we want to use the L command to create a line that draws from our path’s starting point 
    along the x axis for 28px. To do that let’s add our second command: L 46 3. Check your preview 
	and you should see a small horizontal line.</li>
  <li>Now let’s draw a line straight down for 37px by adding L 46 40.</li>
  <li>Then straight to the right by 15px with L 61 40</li>
  <li>Next up we have to begin creating the arrow point. We need to draw a line diagonally down and 
    to the left. We’ll do this with L 32 68.</li>
  <li>And then we’ll have a line go diagonally back up and to the left with L 3 40.</li>
  <li>Now we’ll finish our arrow head by drawing a little ways to the right again with L 18 40.</li>
  <li>To close our shape we don’t need to specify a point to draw a line to. All we need to do is add 
    the Z command, which will automatically close our shape for us.</li>
</ol>

<p>Your final arrow path code should look like this:</p>

```
<path d=" 
M 18 3 
L 46 3 
L 46 40 
L 61 40 
L 32 68 
L 3 40 
L 18 40 
Z 
"></path>
```

<p>For more info on working with <b>&lt;path&gt;</b> check out the references at the bottom of the 
page.</p>

<a href="https://codepen.io/tutsplus/pen/jZbbWG">Codepen.io</a>

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>8. Add <b>&lt;defs&gt;</b> Element</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>We’re all done coding up our six icons, so now we can get them ready for placement and reuse in 
our SVG.</p>

<p>To do this we’re going to wrap the code for all six of our, (presently commented out), icons with 
the tags <b>&lt;defs&gt;&lt;/defs&gt;</b>:</p>

```
<defs>
<!-- All the icons you created so far go in here -->
</defs>
```

<p>This tells the system that all the icons we’ve made are to be hidden by default, until we 
explicitly use them.</p>

<p>You can now uncomment each of your icons and they won’t be seen on the page.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>9. Create Groups With <b>&lt;g&gt;</b></h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>There are two ways we can make our icons ready for use: by converting them to groups, or 
into symbols. We’ll turn the first half of the icons into groups, and the second half into 
symbols so we can illustrate the difference.</p>

<p>To convert one of our icons into a group all we have to do is wrap it with <g></g> tags. To 
make that group usable we also need to give it a unique ID.</p>

<p>For example:</p>

```
<g id="leftalign">
<!-- Left align icon made with lines -->
<line x1="3" y1="3" x2="48" y2="3"></line>
<line x1="3" y1="19" x2="65" y2="19"></line>
<line x1="3" y1="35" x2="48" y2="35"></line>
<line x1="3" y1="51" x2="65" y2="51"></line>
</g>
```

<p>Wrap each of your first three icons with <g></g> tags and add unique IDs, like so:</p>

```
<g id="leftalign">
<!-- Left align icon made with lines -->
<line x1="3" y1="3" x2="48" y2="3"></line>
<line x1="3" y1="19" x2="65" y2="19"></line>
<line x1="3" y1="35" x2="48" y2="35"></line>
<line x1="3" y1="51" x2="65" y2="51"></line>
</g>
<g id="rightcaret">
<!-- Right caret icon made with a polyline -->
<polyline points=" 
3 3 
30 28 
3 53 
"></polyline>
</g>
<g id="browser">
<!-- Browser icon made with rectangle and lines -->
<rect x="3" y="3" width="80" height="60"></rect>
<line x1="3" y1="19" x2="83" y2="19"></line>
<line x1="20" y1="3" x2="20" y2="17"></line>
</g>

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>10. Place Groups With <b>&lt;use&gt;</b></h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>We now have three icons defined as groups in our &lt;defs&gt; element, so we’re ready to use 
them in our SVG. To achieve this, all we need to do is add a <use> element, (being sure to add it 
after and outside the <defs> element), and set an href attribute to target the desired icon’s ID.</p>

<p>For example, to use the left align icon add this code:</p>

```
<use href="#leftalign"></use>
```

<p>To position the icon in a specific location add x and y attributes:</p>

```
<use href="#leftalign" x="100" y="100"></use>
```

<p>The code to add all three icons and space them apart would look something like this:</p>

```
<use href="#leftalign" x="100" y="100"></use>
<use href="#rightcaret" x="300" y="100"></use>
<use href="#browser" x="500" y="100"></use>
```

<p>Check your browser and you should see all three of your first icons:</p>

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>11. Create Symbols With <b>&lt;symbol&gt;</b></h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Instead of using groups to define your icons you can also use symbols. Symbols are almost the 
same as groups, however you gain access to additional settings to control the viewbox and aspect 
ratio.</p>

<p>This can be very useful if you want to do things like centering the icons we’ve created so far. 
We’ll turn the remaining three icons into symbols, then adjust them so they’ll vertically fill a 
100px high space, and be horizontally centered in that space.</p>

<p>We create our symbols in the same way as our groups, only we’ll be wrapping each of our last 
three icons’ code in <symbol></symbol> tags. We’ll also need to add a unique ID to each.</p>

<p>However what we’re also going to add is a viewBox attribute. This will let us define what the 
visible portion of each symbol should be. When the browser has access to this information it can 
then scale and align symbols correctly.</p>

<p>We’ll need to give our <b>viewBox</b> attribute four values. The first two will define the top 
left point of our icon, and the third and fourth define its width and height respectively.</p>

<p>Starting with our “alert” icon, its width and height are both <b>86px</b> so we will set its 
<b>viewBox</b> to <b>0 0 86 86</b> like so:</p>

```
<symbol id="alert" viewBox="0 0 86 86">
<!-- Alert icon made with ellipses and a line -->
<ellipse cx="43" cy="43" rx="40" ry="40"></ellipse>
<ellipse style="fill:black;" cx="43" cy="65" rx="5" ry="5"></ellipse>
<line style="stroke-width: 8;" x1="43" y1="19" x2="43" y2="48"></line>
</symbol>
```

<p>The “play” icon is also <b>86px</b> in width and height, and the “download” icon is <b>64px</b> 
wide by <b>71px</b> high. The corresponding code for our symbols should therefore be:</p>

```
<symbol id="alert" viewBox="0 0 86 86">
<!-- Alert icon made with ellipses and a line -->
<ellipse cx="43" cy="43" rx="40" ry="40"></ellipse>
<ellipse style="fill:black;" cx="43" cy="65" rx="5" ry="5"></ellipse>
<line style="stroke-width: 8;" x1="43" y1="19" x2="43" y2="48"></line>
</symbol>
<symbol id="play" viewBox="0 0 86 86">
<!-- Play icon made with ellipse and polygon -->
<ellipse cx="43" cy="43" rx="40" ry="40"></ellipse>
<polygon points="35 23, 60 43, 35 63" />
</g>
<symbol id="download" viewBox="0 0 64 71">
<!-- Download icon made with path -->
<path d=" 
M 18 3 
L 46 3 
L 46 40 
L 61 40 
L 32 68 
L 3 40 
L 18 40 
Z 
"></path>
</symbol>
```

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>12. Place Symbols With <b>&lt;use&gt;</b></h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>We can now use our symbol icons in the same way as we did our groups. However we’re also going to 
provide each with width and height attributes set to <b>100</b>:</p>

```
<use href="#alert" x="100" y="200" width="100" height="100"></use>
<use href="#play" x="300" y="200" width="100" height="100"></use>
<use href="#download" x="500" y="200" width="100" height="100"></use>
```

<p>You’ll see that each one of your symbol based icons neatly fills and aligns in its <b>100px</b> by 
<b>100px</b> space:</p>

<!-- svg-image-9.png -->

<p>Try applying width and height attributes to the <use> elements of one of your group based icons.
You’ll notice that nothing changes. This is because the browser relies on viewBox values, (which 
a group cannot have), in order to know how to scale the icons.</p>

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3>Wrapping Up</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>That covers the essentials of hand coding SVG! Let’s recap and summarize what we learned:</p>

<ul>
  <li>Setup your <b>&lt;svg&gt;</b> element to wrap your whole graphic.</li>
  <li>Use <b>&lt;line&gt;</b> and <b>&lt;polyline&gt;</b> to create lines.</li>
  <li>Use <b>&lt;rect&gt;</b>, <b>&lt;ellipse&gt;</b> and <b>&lt;polygon&gt;</b> to create closed shapes.</li>
  <li>Use <b>&lt;path&gt;</b> to create anything you want.</li>
  <li>Group shapes with the <b>&lt;g&gt;</b> element.</li>
  <li>For group like behavior with extra features, use <b>&lt;symbol&gt;</b></li>
  <li>Use the <b>&lt;defs&gt;</b> element to define any reusable symbols and groups.</li>
  <li>Place your defined reusable symbols and groups with the <b>&lt;use&gt;</b> element.</li>
</ul>

<p>We learned some solid foundations in this tutorial, but there’s a lot more you can do with SVG 
so don’t stop here, keep digging and discovering more of the awesome things that can be achieved!</p>

<p>In the meantime, hopefully you no longer feel entirely dependent on vector design apps for your 
SVG creation, and you’re confident to produce some of your own graphics by hand. For more complex 
graphics, design apps are still the way to go, but there’s a whole lot you can do with the building 
blocks you have at your disposal, taking advantage of the speed and control hand coding brings.</p>

<ul>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Reference/Element">Complete SVG element reference</a></li>
  <li><a href="https://www.shapes.gallery/"><b>Shapes</b>: Explore the collection of 120+ basic SVG shapes for your upcoming 
    project by monika michalczyk</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Reference/Element/svg"><b>&lt;svg&gt;</b> element reference</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Element/line"><b>&lt;line&gt;</b> element reference</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Element/polyline"><b>&lt;polyline&gt;</b> element reference</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Element/rect"><b>&lt;rect&gt;</b> element reference</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Element/ellipse"><b>&lt;ellipse&gt;</b> element reference</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Element/polygon"><b>&lt;polygon&gt;</b> element reference</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Element/path"><b>&lt;path&gt;</b> element reference</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/d"><b>d attribute</b> reference</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Element/defs"><b>&lt;defs&gt;</b> element reference</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Element/g"><b>&lt;g&gt;</b> element reference</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Element/use"><b>&lt;use&gt;</b> element reference</li>
  <li><a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Element/symbol"><b>&lt;symbol&gt;</b> element reference</li>
</ul>





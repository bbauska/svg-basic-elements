# svg-basic-elements
Basic SVG elements from envato tutorials.

<h2>Basic SVG Elements</h2>
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

<p>As we go through and create our icons, we’ll be working through this list of elements in the order seen above.</p>

<h3>Starter Files</h3>
<p>Before we get started, grab yourself a copy of 
<a href="https://github.com/tutsplus/how-to-hand-code-svg">the starter files from the GitHub repo</a>. 
You can either download a .zip file, or clone the repo to your own system.</p>

<p>We’re going to begin with a document that has some basic HTML and CSS already in place. This will give some styling to the SVGs we’ll be making, and will also set you up with a little grid on the page. We’ll be creating our icons over the top of this grid, and hopefully it will help you visualize the coordinates you’re working with when laying down your SVGs.</p>

<p>When you open up “handcodedsvg.html” from the source “Starter Files” folder you should see the following:</p>

<svg-image-1.png>

<h3>Quick Primer on x and y Values</h3>
<p>When working in 2D space on a website, the horizontal axis is represented by x and the vertical axis is represented by y. Positions along each of these axes are represented by numbers. If we want to move something to the right, we’ll need to use increasing x values, and to move to the left we’ll use decreasing x values. Likewise, to move something down we’ll use increasing y values, and to move something up we’ll use decreasing y values.</p>

<p>A common shorthand for expressing the x and y values of a single point is (x, y). For example, a point at 10 on the x axis and 50 on the y axis might be written as (10, 50). I’ll use this shorthand from time to time in this tutorial.</p>

<p>Notice the two darkest lines on our grid? We’re going to place our SVG so its top left corner aligns with the place they intersect. As such, that intersection point will represent the position x = 0 and y = 0 , or (0,0), in our SVG.</p>

<h3>The Background Grid</h3>
<p>Each of the lightest grid lines represents 10px, and the medium thickness lines represent 100px. So if we wanted to move an object down from one medium thickness line to the next, we’d increase its location on the y axis by one 100px.</p>

<p>If that still sounds a little unclear, don’t worry this will all make sense as we get into the practicalities of creating our SVG icons.</p>

<h3>Default SVG Styling</h3>
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


<h2>1. Setup the SVG</h2>
<p>The first step in creating any SVG is to lay down an <b>&lt;svg&gt;&lt;/svg&gt;</b> element. Anything you want your SVG to display will have to be between these tags. There are a few attributes you can use on this element, but we’ll keep things simple and just use width and height.</p>

<p>Add the following code in the <b>&lt;body&gt;</b> section of your HTML document:</p>

```
<svg width="750" height="500">
</svg>
```

<blockquote>
The CSS in our starter file is going to offset this SVG down and to the right by 100px so its top left corner will be positioned at the intersection point of the two darkest lines on our background grid. And the values in the CodePen demos throughout this tutorial may differ slightly too–but feel free to play around with them.
</blockquote>

<h2>2. Create “Left Align” Icon</h2>
<p>Let’s start by using the <b>&lt;line&gt;</b> element to create this left align icon:</p>

<svg-image-2.png>

<p>The line element has four attributes you’ll need to use:</p>

<ul>
  <li><b>x1</b> horizontal starting point of the line</li>
  <li><b>y1</b> vertical starting point of the line</li>
  <li><b>x2</b> horizontal ending point of the line</li>
  <li><b>y2</b> vertical ending point of the line</li>
</ul>

<p>To summarize the above, you use the <b>x1</b> and <b>y1</b> attributes to set where the line begins, and the 
<b>x2</b> and <b>y2</b> attributes to set where the line ends.</p>

<p>Let’s create the first line of our icon, the one at the top. We’re going to make the line <b>45px</b> long, 
however the <b>5px</b> stroke we’re using is going to add some extra pixels around the outside of our line. 
As such we’ll need to offset our line down and to the right by <b>3px</b> to ensure none of the extra pixels 
created by the stroke are clipped off.</p>

<p>For that reason, we’re going to start our line at a position of <b>3</b> on the <b>x</b> axis and <b>3</b> 
on the <b>y</b> axis. We can set this line starting point of <b>(3,3)</b> by using the attributes <b>x1="3" 
y1="3"</b>.</p>

<p>We want the line to be <b>45px</b> long, so we’re going to add <b>45</b> to our starting <b>x</b> position of 
<b>3</b>, giving us <b>48</b> as the value we want to set for <b>x2</b>. We want the line to finish at the same 
position on the horizontal axis, so we’ll set <b>y2</b> to equal <b>3</b>, i.e. the same value we gave to <b>y1</b>. 
We’ll add this <b>(48,3)</b> line ending point via the attributes <b>x2="48" y2="3"</b>.

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

<p>The <b>y</b> values of each line incrementally increase by <b>16px</b> in order to create the required vertical gap.</p>

<p>Take another look at your browser preview and you should see all four lines. You can also edit the SVG directly in this pen:</p>

<p><a href="https://codepen.io/tutsplus/pen/GQpJNL">CodePen.io example</a>.</p>

<h3>Comment Out Your Icons As We Go</h3>
<p>With that code in place, your first icon is already made. We’re ready to move onto creating the next icon, and we’re going to want to make it in the same position on the grid, but right now the left align icon is in the way. As such, for now just comment out its code to clear the space. We’re going to come back and uncomment it later when we turn our icons into reusable assets.</p>

<p>You’ll need to do the same thing for each icon as we go, commenting it out after you finish creating it. For that reason it’s probably also a good idea to add a little note above the code for each icon so you know which is which when you come back to them later.</p>

<h2>3. Create a “Right Caret” Icon</h2>
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




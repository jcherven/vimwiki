# css-positioning

CSS offers a variety of ways to layout elements and position them on the page.
After watching this video you’ll be able to position elements using CSS. 

The first step in laying out elements is to set its position property. Position
can have one of four values: absolute, fixed, relative and static – which is
the default for all elements. 

The second step in positioning elements is to choose the side for which you
want to position against. Available values are the top, the right, the bottom
or the left side. 

The following is an example of using the fixed position and setting the top to
zero. 

```html
<!DOCTYPE html>
<html>
<head>
  <title>CSS Border</title>
  <style>
    body,html {
      margin: 0;
    }
    
    div {
      position: fixed;
      top: 0;
      width: 100px;
      height: 150px;
      background: #67C067;
    }
    
    .tall {
      height: 400px;
      width: 100%;
      background: brown;
      color: white;
      font-size: 22pt;
      text-align: center;
      padding: 1em 0;
    }
  </style>
</head>
<body>
  <p class="tall">This is a paragraph.</p>
  <p class="tall">This is a 2nd paragraph.</p>
  <p class="tall">This is a 3rd paragraph.</p>
  <div>
    This div is fixed
  </div>
</body>
</html>
```

Relative positioning sets the element relative to its normal flow. In practice,
it is best to set the top and left properties as opposed to trying to set an
element relative to a bottom or right edge. Also of note, elements that are
positioned relative leave blank spaces where they would normally be. In this
example, I have my body tag with div and a paragraph inside of that. I’m going
to set the div position relative. We’ll specify it to be 10 pixels from the top
and offset on the left side by 100 pixels. We’ll still keep a width of 100%, a
height of 150 pixels and we’ll set the background to green.

```html
<!DOCTYPE html>
<html>
<head>
  <title>CSS Positioning (Relative)</title>
  <style>
    div {
      position: relative;
      top: 10px;
      left: 100px;
      width: 100%;
      height: 150px;
      background: #67C067;
    }
    
  </style>
</head>
<body>
  <div>
    <p>This is a paragraph</p>
  </div>
</body>
</html>
```

 Runnings this in a browser, you’ll see that I have my div and its position
 relative to where it would normally have been. It’s offset 10 pixels from the
 top and 100 pixels from the left. 
 
 Absolute positioned elements are set relative to its parent or relative to the
 document body if the parent is positioned statically. This value confuses a
 lot of people in that they forget to set the position of the parent element if
 they want the child to be relative to its parent. 
 
 Let’s get into an example.  Here, I have my body tag and inside of that I have
 a div and a paragraph. In my style tag, I’ve set the div to be positioned
 relative the top and left sides at 0, 100% width. I’ve also set the
 child-paragraph, to have position absolute setting its right and bottom sides
 to zero to align it to the bottom right-hand corner. 
 
```html
<!DOCTYPE html>
<html>
<head>
  <title>CSS Border</title>
  <style>
    div {
      position: relative;
      top: 0;
      left: 0;
      width: 100%;
      height: 150px;
      background: #67C067;
    }
    
    div p {
      position: absolute;
      right: 0;
      bottom: 0;
    }
  </style>
</head>
<body>
  <div>
    <p>This is a paragraph</p>
  </div>
</body>
</html>
``` 
 
 Running this in a browser, you’ll see I have my green div, that’s relatively
 positioned on the page, and my paragraph that’s positioned to the bottom
 right-hand corner of the div. 
 
 Moving on, elements with a fixed position are probably easiest to visualize.
 These elements are relative to the browsing window and will actually scroll
 with the window. 
 
 We’ll demonstrate this with an example. Here, I have my body tag with three
 paragraphs all having the class tall. Using CSS, I’ll specify each paragraph
 to have a height of 400 pixels, a width of 100%, a background of brown so you
 can easily see and distinguish the paragraphs. For the div, we’re going to set
 its position fixed, and set it along the top; indicated by the value of zero
 here. And, we’ve specified a width, a height, and a background color as well. 
 
```html
<!DOCTYPE html>
<html>
<head>
  <title>CSS Border</title>
  <style>
    body,html {
      margin: 0;
    }
    
    div {
      position: fixed;
      top: 0;
      width: 100px;
      height: 150px;
      background: #67C067;
    }
    
    .tall {
      height: 400px;
      width: 100%;
      background: brown;
      color: white;
      font-size: 22pt;
      text-align: center;
      padding: 1em 0;
    }
  </style>
</head>
<body>
  <p class="tall">This is a paragraph.</p>
  <p class="tall">This is a 2nd paragraph.</p>
  <p class="tall">This is a 3rd paragraph.</p>
  <div>
    This div is fixed
  </div>
</body>
</html>
``` 
 
 Running this in our browser, you’ll see that as I scroll the div stays
 positioned along the top of the window. Alright, now, throughout your
 development experience, you may notice that certain elements overlap after
 changing their position. 
 
 To set which element resides on top you can use the z-index. Higher values
 remain on top of lower values. 0 and negative are also valid values for the
 z-index. Using our same example as previously we’re going to change one
 property on our div and that’s the z-index. We’ll set to have a value of
 negative 5. 
 
```html
<!DOCTYPE html>
<html>
<head>
  <title>CSS Border</title>
  <style>
    body,html {
      margin: 0;
    }
    
    div {
      position: fixed;
      top: 0;
      width: 100px;
      height: 150px;
      background: #67C067;
      z-index: -5;
    }
    
    #tall {
      height: 400px;
      width: 100%;
      background: brown;
      color: white;
      font-size: 22pt;
      text-align: center;
      padding: 1em 0;
    }
  </style>
</head>
<body>
  <p id="tall">This is a paragraph.</p>
  <p id="tall">This is a 2nd paragraph.</p>
  <p id="tall">This is a 3rd paragraph.</p>
  <div>
    This div is fixed
  </div>
</body>
</html>
``` 
 
 Running this example, what you’ll see is the fixed div is behind other
 elements. Thus, the red paragraphs, appear to be on top of our fixed div.  
 
 Another property to introduce is the float property. It is used to instruct
 the browser to set an element along the left or right side of its container.
 Valid values are left, right, or none.  Floating an element also allows text
 to wrap around it. So, let’s get into a quick example.  In our body tag, we’ve
 setup a div element that has an id of container. What this is going to do is
 it’s going to contain all of our other divs that we’ll position using the
 float property. In our CSS, we’ll declare the class right to have a float of
 right, and vice versa for the class leftOur container will be set to 100%
 width. 
 
```html
<!DOCTYPE html>
<html>
<head>
  <title>CSS Border</title>
  <style>
    body,html {
      margin: 0;
    }
    
    #container {
      width: 100%;
      background: #9640D0;
      overflow: visible;
    }
    
    .left {
      float: left;
      padding: 1em;
      background: #C49EDF;
    }
    
    .right {
      float: right;
      padding: 1em;
      background: #6B4E7E;
      color: white;
    }
  </style>
</head>
<body>
  <div id="container">
    <div class="left">
      This div is floating left.
    </div>
    
    <div class="right">
      This div is floating right.
    </div>
  </div>
</body>
</html>
``` 
 
 Running this in a browser, you’ll see our div that has the left is floating
 left and the right class is floating right. 
 
 The clear property is used to specify which side or sides to disallow elements
 to float to. You can use values of left, right or both to indicate which side
 or sides to have not have floating elements. Here we’ll demonstrate the clear
 property. On my page, I have a div that’s the same container as before except
 with added an additional div element with a class of clear. To show you the
 styling, our clear has a clear of left and some other properties. 
 
```html
<!DOCTYPE html>
<html>
<head>
  <title>CSS Border</title>
  <style>
    body,html {
      margin: 0;
    }
    
    #container {
      width: 100%;
      background: red;
      overflow: visible;
    }
    
    .left {
      float: left;
      padding: 1em;
      background: #C49EDF;
    }
    
    .right {
      float: right;
      padding: 1em;
      background: #6B4E7E;
      color: white;
    }
    
    .clear {
      float: left;
      background: #DFD09E;
      padding: 1em;
    }
  </style>
</head>
<body>
  <div id="container">
    <div class="left">
      This div is floating left.
    </div>
    <div class="right">
      This div is floating right.
    </div>
    <div class="clear">
      This div has a clear left.
    </div>
    
    
  </div>
</body>
</html>
``` 
 
 What this looks like in the browser, is my div that’s floating left floats
 left. But, then our div that we’ve cleared left, we have essentially forced it
 down to the next block – where that nothing will be on the left side of it.
 Since this div is declared afterwards it is forced below the entire container
 floating to the right still.  
 
 So, let’s play with this a little bit.  Let’s say, we had a clear of right.
 This allows the float to be applied on the left-hand side and then it
 continues to force the last div on the right-hand side below the container.
 Now let’s say we specified clear both. We’ll refresh the page, and it looks
 very similar to the float of left. Next, we’ll rearrange the elements.  As
 opposed to the clear being in the middle, we’ll put the clear at the end.
 Running the example again, you’ll see that the first divs reside inside the
 container floating to their respective sides and the last div with clear both
 applied to it is forced below the other two. 
 
 What if we wanted this div to actually stack in the middle? Well we could
 apply a float of left and it’ll slide next to the first div element. So, we
 have two divs with a float of left.  If we applied a float of left to this one
 it would stack as well. 
 
 Another thing that may occur when changing position or even dimensions of an
 element is that content will overflow outside of its container. The property
 overflow allows you to specify values of hidden to hide content, scroll to
 instruct the browser to add scroll bars around the container, or visible to
 render the overflowing content. You can also use auto as a value to tell the
 browser to fit the content inside of a parent that has a float property
 assigned to it. 
 
 In our example here, we’ll demonstrate the overflow property. In our markup, I
 have the body element with a div and a paragraph with a lot of text. Applied
 to that I have set the font-size to 30 points.  In the CSS, I’ll see the div
 to have a width of 100 pixels and a height of 150 pixels. We’ll set its
 overflow to auto. 
 
```html
<!DOCTYPE html>
<html>
<head>
  <title>CSS Border</title>
  <style>
    body,html {
      margin: 0;
    }
    
    div {
      width: 100px;
      height: 150px;
      background: #67C067;
      overflow: hidden;
    }
    
    p {
      font-size: 30pt;
    }
  </style>
</head>
<body>
  <div>
    <p>This is a really, really, really, really, really, really, really,
    really, really, really, really, really, really, really, long paragraph</p>
  </div>
</body>
</html>
``` 
 
 Running this in a browser you’ll see that any content that flows outside of
 this window, we’re not going to display it. Using auto told the browser to
 display some scroll bars so that we can see the rest of the content. Next
 let’s demonstrate visible.  Refreshing the page, you’ll see that the content
 overflows out of its container. Last we’ll demonstrate hidden. This will hide
 any content that flows outside of its container. 
 
 So, that finishes our lesson on CSS positioning. As a quick recap, you can
 position elements wherever you want in the document flow. Valid values for
 position are static, fixed, absolute or relative. You can use the float
 property to align an element to the right or left side of its container
 allowing text or other elements to wrap around it. And, also, the overflow
 property can specify how content that doesn’t fit inside its parent is
 rendered on the page. 

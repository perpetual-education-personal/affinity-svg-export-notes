# Affinity Designer SVG export notes

Some notes to help explain our desires regarging Affinity Designer SVG export feature requests.

## Goal


**Ultimate goal**: Get as close to our desired final SVG export code as possible, with the least friction.

**Goal of _these notes_**: Clearly explain what currently happens and what we would _like_ to have happen.


## Story

We created a fairly basic graphic.

<img src='images/smiley-with-layers-panel.jpg' alt='Screenshot of Affinity Design project featuring a simple smileyface graphic and displaying the layers of curves it is composed of.'>

note: we normally use tabs, but - github shows them as 4 spaces, so - in this case, we've set them to 2 spaces to make the code more readable.


## Transforms

**note** When an object is moved, AD will create a group and apply a transform to that group. We believe that this is for the sake of the history panel, which is _great_. However - having them in the output makes for mojor trouble in later animatable elements. `flatten transforms [x]` takes care of that smoothly.

```html
  <g id="face1" serif:id="face">
    <g id="skin" transform="matrix(1,0,0,1,5.797,-25.2035)">
      <circle cx="494.203" cy="525.203" r="422.83" style="fill:rgb(255,209,0);"/>
    </g>
    
    <circle id="light" cx="468.312" cy="461.347" r="348.022" style="fill:white;fill-opacity:0.24;"/>
    
    <g id="mouth" transform="matrix(1,0,0,1,-2.75032,-26.3146)">
      <path d="M233.353,606.078C333.242,832.111 657.178,823.132 772.147,607.005" style="stroke:black;stroke-width:1px;"/>
    </g>

    <g id="eyes">
      <g id="eye">
        <g id="white" transform="matrix(1,0,0,1,0,-6.23261)">
          <ellipse cx="362.343" cy="393.68" rx="55.561" ry="85.158" style="fill:white;"/>
        </g>
      <g id="iris" transform="matrix(1,0,0,1.2899,0,-142.347)">
        <circle cx="362.441" cy="417.474" r="30.026"/>
      </g>
    </g>
    ...
```

So, with that out of the way: 

(assumes some ideal output settings) ($todo - note those here)

Here's the AD best AD output (we think/so far)


```html
<?xml version="1.0" encoding="UTF-8" standalone="no"?><!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd"><svg width="100%" height="100%" viewBox="0 0 1000 1000" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xml:space="preserve" xmlns:serif="http://www.serif.com/" style="fill-rule:evenodd;clip-rule:evenodd;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:1.5;"><rect id="face" x="0" y="0" width="1000" height="1000" style="fill:none;"/><g id="face1" serif:id="face"><circle id="skin" cx="500" cy="500" r="422.83" style="fill:#ffd100;"/><circle id="light" cx="468.312" cy="461.347" r="348.022" style="fill:#fff;fill-opacity:0.24;"/><path id="mouth" d="M230.603,579.763c99.888,226.033 423.824,217.054 538.794,0.928" style="stroke:#000;stroke-width:1px;"/><g id="eyes"><g id="eye"><ellipse id="white" cx="362.343" cy="387.447" rx="55.561" ry="85.158" style="fill:#fff;"/><ellipse id="iris" cx="362.441" cy="396.152" rx="30.026" ry="38.731"/></g><g id="eye1" serif:id="eye"><ellipse id="white1" serif:id="white" cx="555.561" cy="387.447" rx="55.561" ry="85.158" style="fill:#fff;"/><ellipse id="iris1" serif:id="iris" cx="555.659" cy="396.152" rx="30.026" ry="38.731"/></g></g></g></svg>
```



This has been indented to show multiline:

```html
<?xml version="1.0" encoding="UTF-8" standalone="no"?>

<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<svg width="100%" height="100%" viewBox="0 0 1000 1000" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xml:space="preserve" xmlns:serif="http://www.serif.com/" style="fill-rule:evenodd;clip-rule:evenodd;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:1.5;">

  <rect id="face" x="0" y="0" width="1000" height="1000" style="fill:none;"/>

  <g id="face1" serif:id="face">

    <circle id="skin" cx="500" cy="500" r="422.83" style="fill:#ffd100;"/><circle id="light" cx="468.312" cy="461.347" r="348.022" style="fill:#fff;fill-opacity:0.24;"/>

    <path id="mouth" d="M230.603,579.763c99.888,226.033 423.824,217.054 538.794,0.928" style="stroke:#000;stroke-width:1px;"/>

    <g id="eyes">
      <g id="eye">
        <ellipse id="white" cx="362.343" cy="387.447" rx="55.561" ry="85.158" style="fill:#fff;"/>

        <ellipse id="iris" cx="362.441" cy="396.152" rx="30.026" ry="38.731"/>
      </g>

      <g id="eye1" serif:id="eye">
        <ellipse id="white1" serif:id="white" cx="555.561" cy="387.447" rx="55.561" ry="85.158" style="fill:#fff;"/>

        <ellipse id="iris1" serif:id="iris" cx="555.659" cy="396.152" rx="30.026" ry="38.731"/>
      </g>
    </g>
  </g>

</svg>
```

note: `id="eye1" serif:id="eye"`

Serif does a thoughtful thing here. When there are 2 things with the same _name_ (layer name) it will add a number because there can only be 1 ID per page. Then it will also move that duplicate ID to a custom attribute as to not delete it. Which is nice of them.

note: the _symbol_ is treated as a group in the output and does not employ a symbol/use or viewBox

## What is needed

This will depend on the person and project. The workflow we use most involves getting these ready to be used on websites as inline SVG graphics or as an img src. (please let us know if this would benefit from more detail)

## What is nessesary

* The SVG itself
* * the viewbox
* * (IF) it's going to be used as an img src then it has to have the xml namespace
* * width and height presentation attributes would be nice
* The paths/curves/shapes - and groups

### What we don't need

* XML version (because the HTML interpreter takes care of that)
* The doctype
* SVG
* * version
* * xlink
* * space (depricated)
* * serif link (we like that shout-out / but for file size - we'd strip it out for production)
* * the inline styles - would be better off as presentation attributes where possible: so that they have the least strenth in the CSS cascade
* Paths and things
* * The artboard isn't doing much for us
* * * we would prefer it's name be the ID of the SVG instead and leave out the rect all together.
* * `style="fill:yellow;"` again - would be better off as `fill:yellow;`

## next steps

This SVG is pretty simple. We could chop this up a bit by hand. We're not afraid to do some work! :) However, sometimes the graphics are much more complex - and we're making a LOT of them.

Theres a tool that can do a lot of this programatically: [SVGO](https://github.com/svg/svgo) (which we assume Serif is aware of) and then also this GUI for SVGO [SVGOMG](https://jakearchibald.github.io/svgomg/).

So, - we currently run it through there:

<img src='images/smiley-in-omg.jpg' alt='Screenshot of the SVG OMG user interface with many toggle switches that can strip out various parts of the SVG code. Updated code is shown on the left and the list of option toggles is on the right.'>

This is what happens after that:

(based on the settings we chose: did we miss some?)

```html
<svg viewBox="0 0 1000 1000" xml:space="preserve" fill-rule="evenodd" clip-rule="evenodd" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="1.5">
  <path id="face" fill="none" d="M0 0h1000v1000H0z"/>
  <g id="face1">
    <circle id="skin" cx="500" cy="500" r="422.83" fill="#ffd100"/>
    <circle id="light" cx="468.31" cy="461.35" r="348.02" fill="#fff" fill-opacity=".24"/>
    <path id="mouth" d="M230.6 579.76c99.9 226.04 423.83 217.06 538.8.93" stroke="#000" stroke-width="1"/>
    <g id="eyes">
      <g id="eye">
        <ellipse id="white" cx="362.34" cy="387.45" rx="55.56" ry="85.16" fill="#fff"/>
        <ellipse id="iris" cx="362.44" cy="396.15" rx="30.03" ry="38.73"/>
      </g>
      <g id="eye1">
        <ellipse id="white1" cx="555.56" cy="387.45" rx="55.56" ry="85.16" fill="#fff"/>
        <ellipse id="iris1" cx="555.66" cy="396.15" rx="30.03" ry="38.73"/>
      </g>
    </g>
  </g>
</svg>
```

### Preparing from there

This moves the styles to presentation attributes, serif:ids - and a bunch of things.

* remove space
* not sure about the fill, clip, and stroke settings... (check)
* remove the path for the artboard (move 'face' id to the SVG)
* remove the group that is under the artboard
* change all ids to classes
* note any ids with added numbers eye1 etc, and re-correct by removing the number 
* (way beyond - but note: possibly switch from hex to hsla on export)
* * can be done in the text editor / fill-opacity=".24" == .25 in hsla
* * [Hex to HSL Color Converter package](https://packagecontrol.io/packages/Hex%20to%20HSL%20Color%20Converter)

```html
<svg id="face"
  viewBox="0 0 1000 1000" 
  fill-rule="evenodd" 
  clip-rule="evenodd"
  stroke-linecap="round"
  stroke-linejoin="round"
  stroke-miterlimit="1.5"
>
  <circle class="skin" cx="500" cy="500" r="422.83" fill="#ffd100" />
  <circle class="light" cx="468.31" cy="461.35" r="348.02" fill="#fff" fill-opacity=".24" />

  <path class="mouth" d="M230.6 579.76c99.9 226.04 423.83 217.06 538.8.93" stroke="#000" stroke-width="1" />

  <g class="eyes">
    <g class="eye">
      <ellipse class="white" cx="362.34" cy="387.45" rx="55.56" ry="85.16" fill="#fff" />
      <ellipse class="iris" cx="362.44" cy="396.15" rx="30.03" ry="38.73"/>
    </g>
    <g class="eye">
      <ellipse class="white" cx="555.56" cy="387.45" rx="55.56" ry="85.16" fill="#fff" />
      <ellipse class="iris" cx="555.66" cy="396.15" rx="30.03" ry="38.73" />
    </g>
  </g>
</svg>
```

Here's what we _might_ end up doing in the end with a bunch of bells and whistles:

(any _unusual_ indentation/formatting to help readability in this README context)

```html
<svg id="face_svg"
  viewBox="0 0 1000 1000" 
  fill-rule="evenodd" 
  clip-rule="evenodd"
  stroke-linecap="round"
  stroke-linejoin="round"
  stroke-miterlimit="1.5"
>
  <defs>
    <style>
      #face_svg {
        --skin: hsl(49, 100%, 50%);
        --light: hsla(0, 0%, 100%, .24);
        --white: hsl(0, 0%, 100%);
        --iris: hsl(0, 0%, 0%);
        --mouth: hsl(0, 0%, 0%);
      }
      #face_svg .skin {
        fill: var(--skin);
      }
      #face_svg .light { fill: var(--light); }
      #face_svg .white { fill: var(--white); }
      #face_svg .iris { fill: var(--iris); }
      #face_svg .mouth { fill: var(--mouth); }

      @keyframes movement {
        50% {
          transform: translate(4%, 0);
        }
        /* does this become global? */
      }

      @media (prefers-color-scheme: dark) {
        #face_svg {
          --skin: navy;
          --light: hsla(0, 0%, 100%, .1);
          --white: hsla(0, 0%, 100%, .6);
          --mouth: hsla(0, 0%, 100%, .4);
          /* bad example colors */
          /* but you might want to change the saturation in some cases */
        }
        #face_svg .light {
          animation: 4s movement infinite ease-in-out;
          /* just to show it's a possibility
          and that they may need to be layered vs. subtracted boolean operations/pathfinder */
        }
      }
    </style>
  </defs>

  <circle class="skin"
    cx="500" cy="500" r="422.83" fill="#ffd100" />
  <circle class="light"
    cx="468.31" cy="461.35" r="348.02" fill="hsla(0, 0%, 100%, .24)" />

  <path class="mouth" 
    d="M230.6 579.76c99.9 226.04 423.83 217.06 538.8.93" stroke="#000" stroke-width="1" />

  <g class="eyes">
    <g class="eye">
      <ellipse class="white"
        cx="362.34" cy="387.45" rx="55.56" ry="85.16" fill="#fff" />
      <ellipse class="iris" 
        cx="362.44" cy="396.15" rx="30.03" ry="38.73"/>
    </g>

    <g class="eye">
      <ellipse class="white"
        cx="555.56" cy="387.45" rx="55.56" ry="85.16" fill="#fff" />
      <ellipse class="iris"
        cx="555.66" cy="396.15" rx="30.03" ry="38.73" />
    </g>
  </g>
</svg>
```

Plese see <a href='https://codepen.io/perpetual-education/pen/KKZWEvo?editors=1100' target='cp1'>a CodePen of this example</a>.

This would also likely have an aria-role='img,' a title, possible a desc, and use aria-labelledby - however, we wouldn't expect the SVG output to deal with any of that.

<hr>

If there's a global class in the context, then something like `.light` or `.white` might leak into this. We tried many things to scope to the SVG and looked into some XML stuff / but no wins yet. 

You could establish an official unique id for the graphic, and use it to prefix all of the classes.

Some people will want to prefix their classes like this:

```html
<svg id="face_svg"
  viewBox="0 0 1000 1000" 
  ...
>
  <defs>
    ...
  </defs>

  <circle class="face_svg-skin"
    cx="500" cy="500" r="422.83" fill="#ffd100" />
  <circle class="face_svg-light"
    cx="468.31" cy="461.35" r="348.02" fill="hsla(0, 0%, 100%, .24)" />

  <path class="face_svg-mouth" 
    d="M230.6 579.76c99.9 226.04 423.83 217.06 538.8.93" stroke="#000" stroke-width="1" />

  <g class="face_svg-eyes">
    <g class="face_svg-eye">
      <ellipse class="face_svg-white"
        cx="362.34" cy="387.45" rx="55.56" ry="85.16" fill="#fff" />
      <ellipse class="face_svg-iris" 
        cx="362.44" cy="396.15" rx="30.03" ry="38.73"/>
    </g>

    <g class="face_svg-eye">
      <ellipse class="face_svg-white"
        cx="555.56" cy="387.45" rx="55.56" ry="85.16" fill="#fff" />
      <ellipse class="face_svg-iris"
        cx="555.66" cy="396.15" rx="30.03" ry="38.73" />
    </g>
  </g>
</svg>
```

```css
<style>
  .face_svg-skin {}
  .face_svg-light {}
</style>
```
It's highly unlikely that there will be any clashes here.

and you could get wild and be extra sure:

```css
<style>
  #face-1357_svg .face_svg-skin {}
</style>
```
If you were working on massive amounts of graphics for a huge company with a ton of different teams working on it. But that's unlikely to be nessesary.


## other thoughts

### An option to include things as symbols in the output / and insert _use_ in their place

<img src='images/symbol-note.png' alt=''>

In some cases - you use the symbols for ease of authoring. You might not want to actually use them in the output. For example, if you wanted to animate the eye pupuls (we named them wrong?) - pupils/iris etc -- then you wouldn't want them to be symbols _maybe_. In other situations, having a hundred stars in a graphic would be better off being symbols. So, maybe there's a toggle for that. (is there any reason not to have those strickly defined in defs?)

```html
<!-- symbol discussion example -->
<svg id="eye_svg" viewBox="0 0 1000 1000" style="background-color: #efefef">
  <defs>
    <!-- this would have it's own viewBox calculated maybe -->
    <symbol id="eye">
      <ellipse class="white"
        cx="362.34" cy="387.45" rx="55.56" ry="85.16" fill="#fff" />
      <ellipse class="iris" 
        cx="362.44" cy="396.15" rx="30.03" ry="38.73" fill="#222"/>
    </symbol>

    <style>
      .eye-three .white {
        fill: red;
      }
      /* investigate this a bit */
    </style>
  </defs>

  <!-- how would the placement tranfer to these instead -->
  <use class="eye-one" href="#eye" x="0" y="0" />
  <use class="eye-two" href="#eye" x="150" y="0" />
  <use class="eye-three" href="#eye" x="300" y="0" />
</svg>
```

If you created a graphic with hundreds of stars then 1 symbol would be ideal, right? Maybe you would group them / and animate their opacity or something. So, the `use`es could be in `g`s - and have their own coordinates. 


### Assign many classes based on spaces in title

<img src='images/multiple-classes-note.png' alt=''>

`<circle class="skin  color-400" ...`





## anything else?

Got any ideas? Are we _way off_ on something? Help us clarify this stuff. : )


## questions

- still a bit confused about how "use document resolution" works. We had some situations where our output was changing sizes / and just wanted to double down on understanding why.



<hr />

## Research

- Corel draw, and a little of everything. Using Adobe Illustrator for ~ 20 years. Using Affinity Designer for 8.

- <a href='https://abookapart.com/products/practical-svg' target='aba'>Practical SVG</a> Book with details on output settings - 2016

- Countless CSS/SVG convention talks. Lots of forum conversations.

- <a href='https://www.oreilly.com/library/view/svg-animations/9781491939697' target='o1'>SVG Animation</a> Book - April 2017

- <a href='https://www.oreilly.com/library/view/using-svg-with/9781491921968/' target='o2'>Using SVG with CSS3 and HTML5</a> Book - October 2017

- Various video tutorials that have now seemingly been removed and possibly included in smaller workshop settings.

- <a href='https://frontendmasters.com/courses/svg-essentials-animation/' target='sd'>Sarah Drasner - SVG Essentials & Animation, v1 and v2</a> 2016, 2019

- <a href='https://www.cassie.codes/speaking/getting-started-with-svg-animation/' target='c'>Cassie Evans - SVG Animation Masterclass</a> September 2021

---

## Other discussions

[Affinity Designer feature wishlist](https://github.com/perpetual-education/affinity-designer-wishlist)



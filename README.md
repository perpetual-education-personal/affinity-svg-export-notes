# Affinity Designer SVG export notes

Some notes to help explain our desires regarging Affinity Designer SVG export feature requests.

## Goal


**Ultimate goal**: Get as close to our desired final SVG export code as possible, with the least friction.

**Goal of _these notes_**: Clearly explain what currently happens and what we would _like_ to have happen.

**Ultimate goal:** Get as close to our desired final SVG export code as possible, with the least amount of steps.

**Goal of these notes:** Clearly explain what currently happens and what we would _like_ to have happen.

## Story

We created a fairly basic graphic.

<img src='images/smiley-with-layers-panel.jpg' alt='Screenshot of Affinity Design project featuring a simple smileyface graphic and displaying the layers of curves it is composed of.'>


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

We could chop this up a bit by hand. We're not afraid to do some work! :)

But - theres a tool that can do a lot of this: [svgomg](https://jakearchibald.github.io/svgomg/)

So, - we'd run it through there:

<img src='images/smiley-in-omg.jpg' alt='Screenshot of the SVG OMG user interface with many toggle switches that can strip out various parts of the SVG code. Updated code is shown on the left and the list of option toggles is on the right.'>


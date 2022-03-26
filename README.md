# Affinity Designer SVG export notes

Some notes to help explain our desires regarging Affinity Designer SVG export feature requests.

## Goal

Ultimate goal: Get as close to our desired final SVG export code as possible, with the least amount of step.
Goal of these notes: Clearly explain what currently happens and what we would _like_ to have happen.

## Story

We created a fairly basic graphic.

<img src='images/smiley-with-layers-panel.jpg' alt='Screenshot of Affinity Design project featuring a simple smileyface graphic and displaying the layers of curves it is composed of.'>

```
<?xml version="1.0" encoding="UTF-8" standalone="no"?><!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd"><svg width="100%" height="100%" viewBox="0 0 1000 1000" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xml:space="preserve" xmlns:serif="http://www.serif.com/" style="fill-rule:evenodd;clip-rule:evenodd;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:1.5;"><rect id="face" x="0" y="0" width="1000" height="1000" style="fill:none;"/><g id="face1" serif:id="face"><circle id="skin" cx="500" cy="500" r="422.83" style="fill:#ffd100;"/><circle id="light" cx="468.312" cy="461.347" r="348.022" style="fill:#fff;fill-opacity:0.24;"/><path id="mouth" d="M230.603,579.763c99.888,226.033 423.824,217.054 538.794,0.928" style="stroke:#000;stroke-width:1px;"/><g id="eyes"><g id="eye"><ellipse id="white" cx="362.343" cy="387.447" rx="55.561" ry="85.158" style="fill:#fff;"/><ellipse id="iris" cx="362.441" cy="396.152" rx="30.026" ry="38.731"/></g><g id="eye1" serif:id="eye"><ellipse id="white1" serif:id="white" cx="555.561" cy="387.447" rx="55.561" ry="85.158" style="fill:#fff;"/><ellipse id="iris1" serif:id="iris" cx="555.659" cy="396.152" rx="30.026" ry="38.731"/></g></g></g></svg>
```

(this has been indented to show multiline)
```
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




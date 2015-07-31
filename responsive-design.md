## Responsive Web Design

#### Set viewport

```html
<head>
	<meta name="viewport" content="width=device-width, initial-scale=1">
</head>
```

---
#### max-width on elements

```css`
img, embed, object, video {
	max-width: 100%;
}
```

---
#### Touch targets

```css
nav a, button {
	min-width: 48px;
	min-height: 48px;
	padding: 1.5em;
}
```

---
#### CSS media queries

```html
<link rel="stylesheet" media="screen and (min-width: 500px)" href="over500.css">
```
```css
@media screen and (min-width: 500px) and (max-width: 960px) {}
```

---
#### Flexbox design pattern

- source code for mobile-first 3-columns layout with full-width header and footer, implemented using flexbox:  
[https://github.com/moodcheerful/memo/blob/master/responsive-design-flexbox-holy-grail.html](https://github.com/moodcheerful/memo/blob/master/responsive-design-flexbox-holy-grail.html)

- view the responsiveness of the above html page in a browser:  
[http://htmlpreview.github.io/?https://github.com/moodcheerful/memo/blob/master/responsive-design-flexbox-holy-grail.html](http://htmlpreview.github.io/?https://github.com/moodcheerful/memo/blob/master/responsive-design-flexbox-holy-grail.html)

---
#### Off-canvas drawer design pattern

- source code for mobile-first off-canvas drawer layout:  
[https://github.com/moodcheerful/memo/blob/master/responsive-design-off-canvas.html](https://github.com/moodcheerful/memo/blob/master/responsive-design-off-canvas.html)

- view the responsiveness of the above html page in a browser:  
[http://htmlpreview.github.io/?https://github.com/moodcheerful/memo/blob/master/responsive-design-off-canvas.html](http://htmlpreview.github.io/?https://github.com/moodcheerful/memo/blob/master/responsive-design-off-canvas.html)

---
#### Responsive tables

- hidden columns:

	```css
	@media screen and (max-width: 500px) {
		.hidden {
			display: none;
		}
	}
	```

- contained horizontal scroll:

	```css
	div.contained_table {
		width: 100%;
		overflow-x: auto;
	}
	```

- no columns, all data formatted with pseudo `before` selector:

	```css
	@media all and (max-width: 500px){
		/* stop table behavior */
		table, thead, tbody, th, td, tr {
			display: block;	
		}
		/* hide table header */
		thead tr {
			position: absolute;
			top: -9999px;
			left: -9999px;
		}
		/* make room for data headers */
		td {
			position: relative;
			padding-left: 50%;
		}
		/* add row lables */
		td:before {
			position: absolute;
			left: 5px;
			content: attr(data-th);
			font-weight: bold;
		}
	}
	```	
	```html
	<table>
		<thead></thead>
		<tbody>
			<tr>
				<td data-th="label"></td>
			</tr>
		</tbody>
	</table>		
	```

---
#### Fonts

- ideal measure (the length of the line of text): 65 characters per line
- font size:

	```css
	.goodFont {
		font-size: 16px;
		line-height: 1.2em;
	}
	.biggerFont {
		font-size: 18px;
		line-height: 1.25em;
	}
	.smallFont {
		font-size: 14px;
		line-height: 1.2em;
	}
	```

---
#### Truncate lines with ellipsis

- ellipsis after one line:

	```css
	.one-line-ellipsis {
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
	}
	```

- ellipsis after multiple lines:

	```css
	.multiple-lines-ellipsis {
		display: block;
		display: -webkit-box;
		display: -moz-box;
		-webkit-line-clamp: 3;
		-webkit-box-orient: vertical;
		/* Firefox needs separate solution for line clamping */
		overflow: hidden;
		text-overflow: ellipsis;
	}
	```

---
#### Responsive images

- use `calc` to space 3 images across the viewport:

	```css
	img {
		float: left;
		margin-right: 10px;
		width: calc((100% - 2*10px)/3);
	}
	img:last-of-type {
		margin-right: 0;
	}
	```

- viewport units: `vh`, `vw`, `vmin = min(vh, vw)`, `vmax = max(vh, vw)`

	```css
	img { 
		max-height: 100vh; 
	}
	```

- raster: use `jpeg`; vector: use `svg`, or `png` if no `svg`, but not `gif`

- caption:

	```html
	<figure>
		<img src="path/to/image.jpg">
		<figcaption>here is the caption</figcaption>
	</figure>
	```

- conditionally load device-specific images for large screens only:

	```css
	@media (max-width: 500px) {
	   .image {
	      background-image: none;
	   }
	}
	@media (min-width: 501px) {
	   .image {
	      background-image: url(image.jpg);
	   }
	}
	```

- glyphs: [Unicode character sets](http://unicode-table.com/en/sets/)











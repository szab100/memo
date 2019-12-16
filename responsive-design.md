## :scissors: Responsive Web Design

#### Set viewport

```html
<head>
	<meta name="viewport" content="width=device-width, initial-scale=1">
</head>
```

---
#### max-width on elements

```css
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

- :computer: view the responsiveness of the above html page in a browser:  
[http://htmlpreview.github.io/?https://github.com/moodcheerful/memo/blob/master/responsive-design-flexbox-holy-grail.html](http://htmlpreview.github.io/?https://github.com/moodcheerful/memo/blob/master/responsive-design-flexbox-holy-grail.html)

---
#### Off-canvas drawer design pattern

- source code for mobile-first off-canvas drawer layout:  
[https://github.com/moodcheerful/memo/blob/master/responsive-design-off-canvas.html](https://github.com/moodcheerful/memo/blob/master/responsive-design-off-canvas.html)

- :computer: view the responsiveness of the above html page in a browser:  
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

## :art: Responsive images

#### Use `calc`:

- example of spacing 3 images across the viewport:

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

---

#### Viewport units:

- `vh`, `vw`, `vmin = min(vh, vw)`, `vmax = max(vh, vw)`

	```css
	img {
		max-height: 100vh;
	}
	```

---

#### File formats:

- raster: use `jpeg`
- vector: use `svg`, or `png` if no `svg`, but not `gif`

---

#### Caption:

```html
<figure>
	<img src="path/to/image.jpg">
	<figcaption>here is the caption</figcaption>
</figure>
```

---

#### Conditionally load device-specific images for large screens only:

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

---

#### Glyphs:

- [Unicode character sets](http://unicode-table.com/en/sets/)

	```html
	<head>
		<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<style type="text/css">
			span {
				font-size: 30px;
			}
		</style>
	</head>
	<body>
		<span>&#119070;</span>
	</body>
	```

---

#### CSS icon fonts:

- [We Love Icon Fonts](http://weloveiconfonts.com/)
- [Font Awesome:](http://fortawesome.github.io/Font-Awesome/)

	```html
	<head>
		<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.4.0/css/font-awesome.min.css">
		<style type="text/css">
			.fa {
				color: red;
			}
		</style>
	</head>
	<body>
		<i class="fa fa-youtube-play"></i>
	</body>
	```

- [Zocial:](http://zocial.smcllns.com/)

	```html
	<!doctype html>
	<html>
	<head>
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<style type="text/css">
			@import url(http://weloveiconfonts.com/api/?family=zocial);

			[class*="zocial-"]:before {
				display: inline-block;
				font-family: 'zocial', sans-serif;
				text-shadow: 3px 3px 3px #aaa;
				width: 1.75em;
			}
		</style>
	</head>
	<body>
		<p class="zocial-facebook">Sign in with Facebook</p>
		<p class="zocial-twitter">Follow me on Twitter</p>
		<p class="zocial-amazon">Buy at Amazon</p>
		<p class="zocial-skype">Skype me</p>
		<p class="zocial-dropbox">Sync with Dropbox</p>
		<p class="zocial-reddit">Share on Reddit</p>
	</body>
	</html>
	```

---

#### srcset

- device pixel ratio:

	```html
	<img src="image_2x.jpg" srcset="image_2x.jpg 2x, image_1x.jpg 1x" alt="Name">
	```

- image size:

	```html
	<img src="large.jpg" srcset="small.jpg 400w, medium.jpg 800w, large.jpg 1020w" alt="Name">
	```

- srcset with sizes:

	```html
	<img src="pic_800.jpg" sizes="(max-width: 400px) 100vw, (min-width: 401px) 50vw" srcset="pic_400.jpg 400w, pic_800.jpg 800w" alt="Name">
	```

---

#### `<picture>` element:

- with media attribute:

	```html
	<picture>
		<source media="(min-width: 800px)" srcset="images-large.jpg">
		<source media="(min-width: 500px)" srcset="image-mid.jpg">
		<img src="image-small.jpg" alt="Name">
	</picture>
	```

- with type attribute:

	```html
	<picture>
		<source srcset="logo.svg" type="image/svg+xml">
		<img src="logo.png" alt="Name">
	</picture>
	```

- with device pixel ratio:

	```html
	<picture>
		<source media="(min-width: 800px)" srcset="images-large-1600_2x.jpg 2x, images-large-800_1x.jpg">
		<source media="(min-width: 500px)" srcset="image-mid.jpg">
		<img src="image-small.jpg" alt="Name">
	</picture>
	```

---

#### ImageMagick:

- install ImageMagick: `brew install imagemagick`

- `convert` options summary:
<http://www.imagemagick.org/script/convert.php>

- run `convert.sh` script to resize an image:
```
#!/bin/bash

SRC="$1"
LOW=60
convert $SRC.jpg -quality $LOW "$SRC"_low.jpg
convert $SRC.jpg -quality $LOW -resize 50% "$SRC"_"$LOW"q_50pc.jpg

# To run the script in a folder containing an image foo.jpg:
# bash convert.sh foo
# or
# chmod u+x convert.sh
# ./convert.sh foo
```

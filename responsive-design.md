### Responsive Web Design

- setting `viewport`:

```html
<head>
	<meta name="viewport" content="width=device-width, initial-scale=1">
</head>
```

- `max-width` on elements in CSS:

```css
img, embed, object, video {
	max-width: 100%;
}
```

- touch targets:

```css
nav a, button {
	min-width: 48px;
	min-height: 48px;
	padding: 1.5em;
}
```

- CSS `media` queries:

```html
<link rel="stylesheet" media="screen and (min-width: 500px)" href="over500.css">
```
```css
@media screen and (min-width: 500px) and (max-width: 960px) {}
```

- CSS `flexbox` pattern:

	- source code for mobile-first 3-columns layout with full-width header and footer, implemented using flexbox:  
	[https://github.com/moodcheerful/memo/blob/master/responsive-design-flexbox-holy-grail.html](https://github.com/moodcheerful/memo/blob/master/responsive-design-flexbox-holy-grail.html)

	- view the responsiveness of the above html page in a browser:  
	[http://htmlpreview.github.io/?https://github.com/moodcheerful/memo/blob/master/responsive-design-flexbox-holy-grail.html]
(http://htmlpreview.github.io/?https://github.com/moodcheerful/memo/blob/master/responsive-design-flexbox-holy-grail.html)

- CSS off-canvas drawer pattern:

	- source code for mobile-first off-canvas drawer layout:  
	[https://github.com/moodcheerful/memo/blob/master/responsive-design-off-canvas.html](https://github.com/moodcheerful/memo/blob/master/responsive-design-off-canvas.html)

	- view the responsiveness of the above html page in a browser:  
	[http://htmlpreview.github.io/?https://github.com/moodcheerful/memo/blob/master/responsive-design-off-canvas.html]
(http://htmlpreview.github.io/?https://github.com/moodcheerful/memo/blob/master/responsive-design-off-canvas.html)

- responsive tables:

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

- fonts:

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



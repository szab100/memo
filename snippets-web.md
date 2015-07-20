### Responsive Design

- set viewport:

```html
<head>
	<meta name="viewport" content="width=device-width, initial-scale=1">
</head>
```

- max-width on elements in CSS:

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

- CSS media queries:

```html
<link rel="stylesheet" media="screen and (min-width: 500px)" href="over500.css">
```
or 

```css
@media screen and (min-width: 500px) and (max-width: 960px) {}
```

- CSS Flexbox:

	- Source code for mobile-first 3-columns layout with full-width header and footer, implemented using flexbox:  
	[https://github.com/moodcheerful/memo/blob/master/snippets-flexbox-holy-grail.html](https://github.com/moodcheerful/memo/blob/master/snippets-flexbox-holy-grail.html)

	- View the responsiveness of the above html page in a browser:  
	[http://htmlpreview.github.io/?https://github.com/moodcheerful/memo/blob/master/snippets-flexbox-holy-grail.html]
(http://htmlpreview.github.io/?https://github.com/moodcheerful/memo/blob/master/snippets-flexbox-holy-grail.html)









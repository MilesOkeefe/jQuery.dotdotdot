jQuery.dotdotdot
================

dotdotdot is a jQuery plugin that automatically truncates your text with an ellipsis(...) so that it doesn't overflow its container.

It works just like `overflow:hidden`, just the user knows content has overflown.


Why not use text-overflow?
=========================

The CSS3 `text-overflow:ellipsis` property is promising but currently only works on one line paragraphs, and does not support some older browsers.

This plugin works on one line and multiline paragraphs.


How to Use
==========

Include jQuery.js and dotdotdot.js in the head of your page like

`<head>
  <script src="jquery.js" type="text/javascript"></script>
	<script src="jquery.dotdotdot.js" type="text/javascript"></script>
</head>`

Surround your target element in a 'wrapper' element to use later

`<div id="wrapper">
  <p>Lorem Ipsum is simply dummy text.</p>
</div>`

Call .dotdotdot() on the wrapper element in .ready()

`$(document).ready(function() {
  $("#wrapper").dotdotdot({
		//	configuration goes here
	});
});`

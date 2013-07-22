jQuery.dotdotdot
================

dotdotdot is a jQuery plugin that automatically truncates your text with an ellipsis(...) so that it doesn't overflow its container.

It works just like `overflow:hidden`, just the user knows content has overflown.


Why not use text-overflow?
=========================

The CSS3 `text-overflow:ellipsis` property is promising but currently only works on one line paragraphs, and does not support some older browsers.

This plugin works on one line and multiline paragraphs.

Performing this action in Javascript comes at a performance cost compared to CSS, but until `text-overflow` supports multiple lines and works with most browsers, this is the best solution.


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

Configuration Options
=====================

Pass any of these options in the array passed to the .dotdotdot() call.

In use:

`$(document).ready(function() {
	$("#wrapper").dotdotdot({
		/*	Text to mark the end of the truncated content. Space will be made for it. Defaults to '...', can be any string */
		ellipsis	: '... ',
 
		/*	 How precisely the text will be cut off. Content breaks on 'word', 'letter', or 'children'*/
		wrap		: 'word',
 
		/*	jQuery-selector for the element to keep and put after the ellipsis. */
		after		: null,
 
		/*	Whether to update the ellipsis: true/'window' */
		watch		: false,
	
		/*	Optionally set a max-height, if null, the height will be measured. */
		height		: null,
 
		/*	Deviation for the height-option. */
		tolerance	: 0,
 
		/*	Callback function that is fired after the ellipsis is added,
			receives two parameters: isTruncated(boolean), orgContent(string). */
		callback	: function( isTruncated, orgContent ) {},
 
		lastCharacter	: {
 
			/*	Remove these characters from the end of the truncated text. */
			remove		: [ ' ', ',', ';', '.', '!', '?' ],
 
			/*	Don't add an ellipsis if this array contains 
				the last character of the truncated text. */
			noEllipsis	: []
		}
	});
});
`

Custom Events
=============

Need to update the ellipsis manually? Trigger the "update"-event.

`$("#button").click(function() {
	$("#wrapper").trigger("update");
});`


Want to know if the text got truncated? Trigger the "isTruncated"-event.

`$("#button").click(function() {
	//	by using the return-value...
	var isTruncated = $("#wrapper").triggerHandler("isTruncated");
	if ( isTruncated ) {
		//	do something
	}
	
	//	...or by using the callback function
	$("#wrapper").trigger("isTruncated", function( isTruncated ) {
		if ( isTruncated ) {
			//	do something
		}
	});
});`

Need the original content? Trigger the "originalContent"-event.

`$("#button").click(function() {
	//	by using the return-value...
	var content = $("#wrapper").triggerHandler("originalContent");
	$("#foo").append( content );
	
	//	...or by using the callback function
	$("#wrapper").trigger("originalContent", function( content ) {
		$("#foo").append( content );
	});
});`


If you want to destroy the ellipsis, trigger the "destroy"-event.

`$("#button").click(function() {
	$("#wrapper").trigger("destroy");
});`


Please note that all custom events have been namespaced to ".dot", so to prevent interfering with other scripts, triggering an event would best be done like this:

`$("#wrapper").trigger("update.dot");`

Examples
========

All of these examples are called in the `$(document).ready();` function.

Standard ellipsis truncation:

`$(".ellipsis").dotdotdot();`

Including a 'Read More' link at the end of the truncated content:

`$(".ellipsis").dotdotdot({
	after: "a.read-more"
});`

Have the cut off point adapt when the size of the container changes. Responsive/fluid layouts can utilize this:

`$(".ellipsis").dotdotdot({
	watch: "window"
});`

You can even let dotdotdot truncate your links in a readable way:

`$('.pathname').each(function() {
	var path = $(this).html().split( '/' );
	if ( path.length > 1 ) {
		var name = path.pop();
		$(this).html( path.join( '/' ) + '<span class="filename">/' + name + '</span>' );
		$(this).dotdotdot({
			after: 'span.filename',
			wrap: 'letter'
		});						
	}
});`

so that `www.website.com/that/should/be/truncated/before/the/file.html` turns into `www.website.com/that/should/... /file.html`


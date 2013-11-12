---
layout: default
title: jQuery.sidenotes
---

# jQuery.sidenotes

Transform Markdown footnotes into superpowered[^notes] sidenotes.

[^notes]: Wanna see something cool? Resize this page and watch how this note adapts to different screen sizes.

## Installation

Upload `jquery.sidenotes.min.js` to a server and add it to your document's head:

    <script src="jquery.sidenotes.min.js"></script>

### With Bower

jQuery.sidenotes is available as a [Bower](http://bower.io) package.

    bower install jquery.sidenotes

## Usage

With no configuration (use sensible defaults):

    // Apply to your post/document container(s).
    $('.post').sidenotes();

With options:

    // Pass a options object
    $('.post').sidenotes({
      'removeRefMarkRegex':     /-sn$/,
      'initiallyHidden':        true
    });

### Basic

By default, footnotes are transformed into `aside` elements and placed into the document near their reference.

Please note that, by design, jQuery.sidenotes does not apply any CSS styling. It's up to you to style the generated sidenotes using appropriate selectors.[^style]

[^style]: You can use CSS media queries to target specific screen sizes.

### Advanced

Built-in methods allow you to toggle between footnotes and sidenotes.

    // Hide the sidenotes, show the footnotes
    $('.post').sidenotes('hide');

    // Show the sidenotes, hide the footnotes
    $('.post').sidenotes('show');

This is perfect for responsive designs, where you may only want to use sidenotes when the screen is large enough to accomodate them.

By default, sidenotes are placed *before* their reference in the text. This is due to the expectation that most designers will want to float them so that they are adjacent to their reference. However, if the sidenotes are not floated, it's probably better to place them *after* their reference in the text, so that the note does not appear before the reference. You can update the `sidenotePlacement` property to toggle between the two states.

    // Place the sidenotes after their references
    $('.post').sidenotes('sidenotePlacement', 'after')

    // Place the sidenotes before their references
    $('.post').sidenotes('sidenotePlacement', 'after')

You can set the initial `sidenotePlacement` in the options object.

## Options

jQuery.sidenotes is designed to work with zero configuration while also being highly configurable. You can set the following options by passing them as a JSON object to the plugin constructor.

### initiallyHidden

By default, the sidenotes are shown immediately after they are created during plugin initializaiton. By setting this to `true`, the sidenotes will remain hidden until explicitly shown with `$.fn.asides('show')`.

Default: `false`

### sidenotePlacement

By default, the sidenotes are initially placed *before* their reference in the text, with the expectation that they will be floated. To place them *after* their reference, set this to `'after'`.

Default: `'before'`

### removeRefMarkRegex

Use to enable numberless, or reference-less, sidenotes. Footnote IDs that match this regular expression will be displayed without a number.[^refless-sn] The reference mark in the document will be hidden, and the notes that follow will be renumbered accordingly. When the sidenotes are hidden, the original references are restored.

[^refless-sn]: `removeRefMarkRegex` is `/-sn$/`, and the footnote ID corresponding to this note is `fn:refless-sn`. Therefore, the sidenote is rendered without a reference.

The default regular expression will not match any footnote.

Default: `/(?!)/`

### sidenoteElement

The element type of the sidenotes.

Default: `'aside'`

### sidenoteGroupElement

Sidenotes[^grouped1] that are placed next to each other[^grouped2] in the document are automatically wrapped in a container element. This is the element type of the container.

[^grouped1]: This sidenote and the next one...

[^grouped2]: ... are part of a sidenote group.

Default: `'div'`

### sidenoteClass

The class that is added to each sidenote.

Default: `'sidenote'`

### sidenoteGroupClass

The class that is added to each group.

Default: `'sidenote-group'`

### refMarkClass

The class that is added to each sidenote's reference mark.

Default: `'ref-mark'`

## Addtional options for selectors

There is some variation in how Markdown processors generate the markup for footnotes. The default options have been chosen to work across all of them, but if they do not, trying passing a new `footnoteContainerSelector` or `footnoteSelector` as options. If you're still having problems with your Markdown processor, please submit an issue.

### footnoteContainerSelector

jQuery selector string for the footnote container. This selector is run within the context of the post container.

Default: `'.footnotes'`

### footnoteSelector

jQuery selector string for the footnotes. This selector is run within the context of the footnote container.

Default: `'> ol > li'`

## API

On this page, you can use the following key bindings to test these methods:

* `s`: `$.fn.sidenotes('show')`
* `h`: `$.fn.sidenotes('hide')`
* `b`: `$.fn.sidenotes('sidenotePlacement', 'before')`
* `a`: `$.fn.sidenotes('sidenotePlacement', 'after')`

### $.fn.sidenotes(options)

Sets up the document. Apply to each post/document container. A post container must contain both the content of the post and its footnotes.

Optionally, you can pass an options object.

### $.fn.sidenotes('show')

Shows the sidenotes and hides the footnotes.

### $.fn.sidenotes('hide')

Hides the sidenotes and shows the footnotes.

### $.fn.sidenotes('isHidden')

Returns `true` if the sidenotes are hidden.

### $.fn.sidenotes('sidenotePlacement', placement)

Changes the placement of the sidenotes to either before or after their references in the text. Accepted values are `'before'` or `'after'`.

If no arguments are passed, or if the `placement` argument is invalid, this returns the current `sidenotePlacement`.

### $.fn.sidenotes('destroy')

Destroys the plugin instance. Removes the sidenotes and shows the footnotes.

## Requirements

* jQuery (obviously)
* Markdown-generated content, or markup that mimics it.

## License

Copyright 2013
[Andrew Clark](http://andrewphilipclark.com)

Licensed under the [MIT License](http://opensource.org/licenses/MIT)
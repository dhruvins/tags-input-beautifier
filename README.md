Simplest Tags Input Beautifier
==============================

> Better tags input interaction with JavaScript.

What is this?

Demo
----

![Image](https://cloud.githubusercontent.com/assets/1669261/12162361/7b457e14-b533-11e5-990a-8805cac26bb3.gif)

&rarr; https://tovic.github.io/tags-input-beautifier

Got it?

Usage
-----

~~~ .html
<!DOCTYPE html>
<html dir="ltr">
  <head>
    <meta charset="utf-8">
    <title>Demo</title>
    <link href="tags-input-beautifier.min.css" rel="stylesheet">
  </head>
  <body>
    <input name="tags" type="text">
    <script src="tags-input-beautifier.min.js"></script>
    <script>
    var tags = new TIB(document.querySelector('input[name="tags"]'));
    </script>
  </body>
</html>
~~~

Options
-------

~~~ .js
var tags = new TIB(source, config);
~~~

Variable | Description
-------- | -----------
`source` | The text input element you want to beautify.
`config` | The configuration data. See below!

~~~ .js
config = {
    join: ', ', // Tags joiner of the output value
    max: 9999, // Maximum tags allowed
    escape: [','], // List of character(s) used to trigger the tag addition
    pattern: false, // Custom pattern to filter the tag name [^1]
    placeholder: false, // Custom tags input placeholder [^2]
    alert: true,
    text: ['Delete \u201C%s%\u201D', 'Duplicate \u201C%s%\u201D', 'Please match the requested format: %s%'],
    classes: ['tags', 'tag', 'tags-input', 'tags-output', 'tags-view'], // HTML classes
    update: function() {} // Hook that will be triggered on every tags item update
};

// [^1]: Or simply use `data-pattern` attribute of `source` element.
// [^2]: Or simply use `data-placeholder` or `placeholder` attribute of `source` element.
~~~

Methods
-------

### Initiation

~~~ .js
var tags = new TIB( … );
~~~

### Get Current Tags Data

~~~ .js
console.log(tags.tags);
~~~

### Get Fake Tags Input Element

~~~ .js
console.log(tags.input);
~~~

### Get Tags View HTML Element

~~~ .js
console.log(tags.self);
~~~

### Get Original Tags Input Element

~~~ .js
console.log(tags.output);
~~~

### Get Configuration Data

~~~ .js
console.log(tags.config);
~~~

### Remove All Tags

~~~ .js
tags.reset();
~~~

### Remove _bar_ Tag

~~~ .js
tags.reset('bar');
~~~

### Refresh Tags Value

~~~ .js
tags.update();
~~~

Merge new values to the current values:

~~~ .js
tags.update(['foo', 'bar', 'baz']);
~~~

### Sanitize Tag Name

Create custom tag input sanitizer:

~~~ .js
tags.filter = function(text) {
    text = text.replace(/^\s+|\s+$/g, ""); // trim white-space(s)
    text = text.replace(/,/g, ""); // disallow `,` in tag name
    text = text.toLowerCase(); // force lower-case letter(s)
    return text;
};
~~~

### Add _bar_ Tag

~~~ .js
tags.set('bar');
~~~

### Check for Duplicate Tag Name

~~~ .js
if (tags.tags['bar']) {
    alert('Duplicate `bar` !!!')
}
~~~

### Check for Tags Length

~~~ .js
console.log(Object.keys(tags.tags).length);
~~~

Playground
----------

 - http://codepen.io/tovic/pen/ZQewJq
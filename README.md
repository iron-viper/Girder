Girder CSS [demo](http://comfypixel.com/Girder/)
====================

A CSS grid toolkit built with Sass. Extra handy for HTML prototypes because its small, fast and easy to use. **Why build another CSS grid?** Because I can :) No, really. I couldn't find exactly what I was looking for so I decided to spin my own solution over a rainy weekend. I'm drawing inspiration from all over but really looking to keep things super simple:

* Its Sass with semantic html5 in mind but can also be used with [plain CSS](http://comfypixel.com/Girder/guide.html) (girder.css)
* Conscise but well commented, small, focused and easy to learn. No excess stuff just the essentials.
* Instead of columns it uses flexible grid units based on page sections (.half, .two-thirds).
* The grid likes relative units and can easily adapt to a mobile-first approach (but its not required).
* It makes no other assumptions of how you want to build (its just a layout helper). You bring your own typography, design elements, javascript, plugins, etc.

---

# How it works
Girder is a simple yet versatile grid designed for building with <a href="http://sass-lang.com/">Sass</a>, a fantastic pre-processor. It builds flexible layouts divided into logical sections and uses silent classes (placeholders) to structure content in HTML; this keeps your Markup free of excess presentational (often meaningless) classes like "unit_1of4", "small-2", "grid4". [View the examples](http://comfypixel.com/Girder/example-css.html)

**Sample Code:** You can write HTML with your own classes to target elements or use the cascade:
```HTML
<main class="container row">
	<article>
		<p>The main column covers two thirds of the page.</p>
		<ul>
			<li>One</li>
			<li>Two</li>
			<li>Three</li>
			<li>Four</li>
		</ul>
	</article>
	<aside> This sidebar covers one third of the page. </aside>
</main>
```
The Sass for this example could look like this:
```SCSS
// Adjust unit spacing in pixels, em or rem (optional)
$gutters: 1.25em;
// Containers can be fluid, fixed, centered or whatever you need
$container-width: 1322px;
// Include the main Girder partial
@import girder;

.container {
	article {
		@include unit(two-thirds);
	}
	aside {
		@include unit(third);
		background: #ddd;
	}
	article li {
		@include unit(fourth);

		@include breakpoint($medium-breakpoint) {
			@include responsive-unit(half); // easily change layouts based on screen size
		}
	}
}
```
### Pages built with Girder using a mix of Sass and pure CSS:
* [Setup Guide](http://comfypixel.com/Girder/guide.html)
* [Examples Page](http://comfypixel.com/Girder/example-css.html)
* [Girder-Ghost Theme](http://ghost.fredmaya.com)
* [Portfolio](http://fredmaya.com)

# Setup / Requirements
Copy the Sass folder from this Repo. Or [download the source and example files](https://github.com/unmaya/Girder/archive/master.zip). You only need two things, the main settings file and the modules folder (everything else is optional):

*	**girder.scss**
*	**/girder_modules/**

Include the Girder scss file:
```SCSS
// Customize settings here or directly inside _girder.scss (optional)
@import girder;

// Follow with your base styles
```

1. Unless you're using plain CSS be sure the Compass Gem is installed which includes Sass, if you're not sure, issue this command in the console: ```sudo gem install compass```
2. Start building your markup and hook up the grid simply by adding rows and including the mixins in your selectors like this:

```SCSS
// Units go as small as sixth of any container, mix and match as needed
@include unit(three-fourths); // Three quarters of a page (inc. gutters by default)
@include unit(third, false); // A Third of any container (add 'false' to remove gutters)
.sixth-box {
	@include unit(sixth);

	@include breakpoint('medium screens') {
		@include responsive-unit(third);
	}
}
```

**To use plain CSS** you just add the classes to the markup like this [Example page](http://comfypixel.com/Girder/example-css.html):
```HTML
<!-- Be sure to include the girder.css file in your document -->
<main class="content row">
	<article class="unit two-thirds"> My main column covers two thirds of the page. </article>
	<aside class="unit third"> This sidebar content occupies one third of the page. </aside>
	<footer class="clear">Awesome footer</footer>
</main>
```

**Some familiar options:** Wrap multi-column rows with the ```.row``` class. Nest rows and mix grid units to achieve your desired results. You can remove gutters, push units, add media queries or use any number of plugins for Sass. [Check the example](http://comfypixel.com/Girder/), inspect, poke and download the source to see exactly how it works.

For more tips on using Sass and CSS layout tools like Girder, visit the [dev journal](http://ghost.fredmaya.com).

## Optional
Girder is tiny but it can scale based on your project's needs. It includes support for more complex media queries using the Breakpoint() compass plugin. Just make sure you [install the gem](http://rubygems.org/gems/breakpoint) and include the module by modifying or overwriting these settings:

````SCSS
$use-breakpoint: true;
@import "breakpoint";
````

### This project is open to suggestions, forks, experiments, etc
Open Source Under <a href="http://opensource.org/licenses/MIT">MIT</a> license.
# Best Practices: CSS

Welcome to Happy Medium's internal CSS style guide. We use this for any project involving websites at Happy Medium. You should have a general idea of **specificity** and the [SCSS syntax](http://sass-lang.com/).

This style guide is modeled off of [Github's CSS Styleguide](https://github.com/styleguide/css).

## Coding Style

* Use soft-tabs with a four space indent (for readability).
* Put spaces after `:` in property declarations.
* Put spaces before `{` in rule declarations.
* Use hex color codes `#000` unless using rgba.
* Use `//` for comment blocks (instead of `/* */`).
* Document styles gratuitously (especially since the end-result is stripped and minified).

Here is good example syntax:

```css
// This is a good example!
.styleguide-format {
	border: 1px solid #0f0;
	color: #000;
	background: rgba(0,0,0,0.5);
}
```

## SCSS Style

* Any `$variable` or `@mixin` used in more than one file should be stored in the `/generic` folder. Others can be placed at the top of the file in which they're used.
* As a rule of thumb, don't nest further than three levels deep. If you find yourself going further, think about reorganizing your rules (either the specificity needed, or the layout of the nesting).
* Place any `@include` calls to mixins and nested selectors at the end of parent selector to reduce clutter.

# File Organization

In general, CSS is organized within projects in an atomic-based structure using `/generic`, `/base`, and `/object` folders:

```
/sass/
	/base/
		_global-classes.scss
		_headings.scss
		_links.scss
		_text.scss
		...
	/generic/
		_mixins.scss
		_reset.scss
		_variables.scss
	/objects/
		_buttons.scss
		_carousel.scss
		_cover.scss
		_footer.scss
		_header.scss
		_icons.scss
		_layout.scss
		_lists.scss
		_main.scss
		_nav.scss
		_sections.scss
		_text.scss
```

## Px vs. Ems

Use `ems` for `font-size`, as it can be scaled quickly and efficiently. Additionally, unit-less `line-height` is preferred because it does not inherit a percentage value of its parent element, but instead is based on a multiplier of the `font-size`.

When possible, use `ems` for `margin`, `padding`, and other proportionally-focused attributes. Use `ems` with media queries as well.

For fixed-width and other font-size-independent attributes, consider using `rems` as they aren't effected by the parent container's `font-size`. __Note: You will need to use a rem polyfill to support older browsers.__

Use `px` for `border` and other decorations (`box-shadow`, `text-shadow`).

## Specificity (classes vs. IDs)

Elements that **occur exactly** once inside a page should use IDs, otherwise, use classes. When in doubt, use a class name.

* **Good** candidates for IDs: header, footer, modal popups.
* **Bad** candidates for IDs: navigation, item listings, item view pages (ex: issue view).

When styling a component, start with an element + class namespace (prefer class names over IDs), prefer direct descendant selectors by default, and use as little specificity as possible. Here is a good example:

```html
<ul class="category-list">
	<li class="item">Category 1</li>
	<li class="item">Category 2</li>
	<li class="item"><a href="#">Category 3</a></li>
</ul>

<style type="text/css">
ul.category-list { // element + class namespace

	> li { // direct descendant selector > for list items
		list-style-type: disc;
	}

	a { // minimal specificity for all links
		color: #ff0000;
	}
}
</style>
```

### CSS Specificity Guidelines

Try to follow the [BEM Methodology](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) when building out components in CSS.

* When building out a block, use the BEM selectors to separate different components. Here is an example:

    ```html
	<div class="block block--event">
		<div class="block__thumb">
			<img src="http://..." alt="Thumbnail" />
		</div>
		<div class="block__text">
			<h3 class="block__title"><a href="#">This is a title</a></h3>
			<div class="block__excerpt">
				<p>This is an excerpt</>
			</div>
		</div>
	</div>
	```

* If you must use an id selector (`#selector`) make sure that you have no more than _one_ in your rule declaration. A rule like `#header .search #quicksearch { ... }` is considered harmful.

## Separate Style from Layout

In general, try to separate style from layout. This allows for modular reuse of styles throughout your site while keeping layout independent. Remember: it's easier to add or remove a class from an HTML element than refactor all of your CSS!

```html
<!-- bad example -->
<div class="two-columns--featured">
	<div class="col"></div>
	<div class="col"></div>
</div>

<style type="text/css">
.two-columns--featured {
	background: #efefef;
	font-size: 1.2em;

	> .col {
		width: 48%;
		float: left;
		margin: 0 2%;
	}
}
</style>

<!-- good example -->
<div class="two-columns section--featured">
	<div class="col"></div>
	<div class="col"></div>
</div>

<style type="text/css">
.two-columns {
	> .col {
		width: 48%;
		float: left;
		margin: 0 2%;
	}
}

.section--featured {
	background: #efefef;
	font-size: 1.2em;
}
</style>
```

Remember: End users don't care how your CSS looks, as long as the website looks OK. Think about other _developers_ when you are building and documenting your stylesheets!

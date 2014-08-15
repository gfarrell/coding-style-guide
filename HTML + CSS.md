# HTML + CSS Style Guide

Gideon Farrell <me@gideonfarrell.co.uk>

## HTML

### To line-break or not to line-break

Most elements should have their opening and closing tags on separate lines, at indentation level **x**, with the content at indentation level **x + 1**. The exceptions to this rule are *inline* elements whose character length is less than about 80 characters (there is some flexibility here). So, for example:

	<div>
		<p>Some small amount of content</p>
		<p>
			Larger amounts of content should be broken onto many lines otherwise it looks ugly in the editor and can be hard to find the opening and closing tags
		</p>
	</div>

### Semantic Elements

HTML5 defines lots of semantic elements, like `<header>`, `<section>` and `<nav>`. Where possible, these elements should be used instead of repurposed `<div>`s etc..

### Attributes

When many different attributes are used on elements in a large document, in is helpful to stick to an ordering of these attributes, so that a developer can look at an element, and know more quickly which attributes are present. The ordering I use is as follows:

1. `tag name` (obviously)
2. `id`
3. `class`
4. `rel`, `language`, `type` (if applicable)
5. `src`/`href` (if applicable)
6. `title`/`alt` (if applicable)
7. for form elements: `placeholder`, `required`, `autocomplete` etc.
8. any `data-` attributes
9. anything else

#### Long tag definitions

Sometimes there will be lots of attributes on a tag. In the case of more than four-ish attributes (if the line length exceeds about 80 characters), these attributes should be spread over several lines. One common example from my own experience is `<script>` tags when including AMD modules. These would be broken up as follows:


	<script language="javascript"
			type="text/javascript"
			src="/path/to/require.js"
			data-main="/path/to/main.js">
	</script>

### Demarcating large bodies of HTML with comments

Sometimes you will have a long `<section>` or `<div>` where scrolling to the bottom in your editor might render the top no-longer visible. In these cases (and more generally this is useful), such elements should be surrounded by comments denoting what they are. For example:

	<!-- about us -->
	<section>
		<!-- lots of content -->
	</section>
	<!-- /about us -->

### IDs vs. classes vs. nothing at all

`id` attributes are rarely necessary and should be avoided whenever possible. The reasons for this are threefold: the first is that elements labelled by `id` are not robust to change, because often changes involve changes to document structure; the second is that `id` tags pollute a global namespace; the third (and arguably most important) reason is that `id` attributes are the epitome of specificity and cannot be generalised. Wherever possible, a developer should be looking to generalise code and styling, and the use of `id`s are contrary to the pursuit of this principle.

In most cases, `id` attributes are unnecessary, and can be replaced either by classes or by nothing at all, since they aren't used in-and-of themselves.

## CSS (LESS)

### A word on build products and file organisation

Ideally, all pages should load a single file (let's call it *styles.less*). This should import other files (and not have files defined within it). Files should be separated on the basis of the type of styles they provide. For example, styles relating to fonts, `<p>` elements, `<h*>` elements etc., as well as defining typographical styles, should reside in *typography.less*. For any new project, I normally create the following stylesheets:

* **styles.less** imports all other stylesheets - build product
* **base.less** overall structure, very general. Things like headers, footers, body background colour etc.
* **typography.less** font family, sizing, `<h*>` styles, `<p>`, etc.. Font colours, styles.
* **forms.less** styling for form controls (and overrides)
* **lists.less** lists are used all the time, this commonly includes a `ul.horizontal` class.
* and so on

Individual UI components should have their own stylesheets, prefixed with *ui-*. So, for example, had I a profile card component, the styles governing it would reside in *ui-profile-card.less* and be referenced from *styles.less* if there aren't too many, or possibly a *ui.less* stylesheet, which in turn would be included in *styles.less*. This allows sufficient modularity.

**We should always try to reduce the number of build products.** The reason for this is that, while it may be tempting to *only* load the CSS pertinent to the page at hand, this makes for very inefficient caching. All pages will have common styles, like the grid system, headers, footers, etc.. Where we to have individual build products for different pages (or even different types of page) then these common resources would be loaded over and over again. The overhead from HTTP requests to load these resources far outweighs the benefits of loading only pertinent CSS. Rolling the whole app into a single build product also makes sure that theses styles are cached and can be used anywhere. This approach is even more valid when supported by a strong generalisation urge in your development.
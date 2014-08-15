# HTML + CSS Style Guide

Gideon Farrell <me@gideonfarrell.co.uk>

## HTML Semantic Elements

HTML5 defines lots of semantic elements, like `header`, `section` and `nav`. Where possible, these elements should be used instead of repurposed `div`s. 

## HTML Attributes

When many different attributes are used on elements in a large document, in is helpful to stick to an ordering of these attributes, so that a developer can look at an element, and know more quickly which attributes are present. The ordering I use is as follows:

1. `tag name` (obviously)
1. `id`
1. `class`
1. `rel`, `language`, `type` (if applicable)
1. `src`/`href` (if applicable)
1. `title`/`alt` (if applicable)
1. for inputs: `placeholder`, `required`, `autocomplete` etc.
1. any `data-` attributes


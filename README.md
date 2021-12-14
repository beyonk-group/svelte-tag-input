<a href="https://beyonk.com">
    <br />
    <br />
    <img src="https://user-images.githubusercontent.com/218949/144224348-1b3a20d5-d68e-4a7a-b6ac-6946f19f4a86.png" width="198" />
    <br />
    <br />
</a>

## Beyonk Tag Input

[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com) [![svelte-v3](https://img.shields.io/badge/svelte-v3-blueviolet.svg)](https://svelte.dev) ![publish](https://github.com/beyonk-adventures/svelte-tag-input/workflows/publish/badge.svg)

## Demo

View a [demo page](https://docs-tag-input.vercel.app/).

## Usage

Installation:

```bash
npm i -D @beyonk/svelte-tag-input
```

## Props

There are a couple of properties you can pass to the tag input:

### tags

An array containing preexisting tags for the input. Bind to this to keep your array up to date with changes:

```svelte
<script>
  let myTags = [ 'foo', 'bar' ]
</script>

<TagInput bind:tags={myTags}>
```

### colour={function}

A function which takes the tag content as the only parameter and uses it to generate a CSS colour. The default function creates a hashcode from the tag content and creates a pastel colour based on it.

### delimiter

The delimiter which, when pressed, will create a new tag from the current content. Duplicate tags are not added.

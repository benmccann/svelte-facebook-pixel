<a href="https://beyonk.com">
    <br />
    <br />
    <img src="https://user-images.githubusercontent.com/218949/144224348-1b3a20d5-d68e-4a7a-b6ac-6946f19f4a86.png" width="198" />
    <br />
    <br />
</a>

## Svelte Facebook Pixel Component

[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com) [![CircleCI](https://circleci.com/gh/beyonk-adventures/svelte-facebook-pixel.svg?style=shield)](https://circleci.com/gh/beyonk-adventures/svelte-facebook-pixel) [![Svelte v3](https://img.shields.io/badge/svelte-v2-orange.svg)](https://v2.svelte.dev) [![Svelte v3](https://img.shields.io/badge/svelte-v3-blueviolet.svg)](https://svelte.dev)


Facebook pixel tracking component for Svelte.

## Install

```bash
$ npm install --save-dev @beyonk/svelte-facebook-pixel
```

## Usage

```html
<FacebookPixel bind:this={fb} id={123} />

<script>
  import FacebookPixel from '@beyonk/svelte-facebook-pixel'
</script>
```

You can import FacebookPixel component whenever and wherever you want, the facebook tracking code is only initialised in the first instance.

### Tracking

Simply call the track mehtod:


```html
<FacebookPixel bind:this={fb} />

<script>
	import FacebookPixel from '@beyonk/svelte-facebook-pixel'
	import { onMount } from 'svelte
	
	let fb

	onMount(() => {
		fb.track('SomeEvent', { some: 'data' })
	})
</script>
```

### Multiple Pixels on a page

You can have multiple pixels on a page, for instance, if you need a backup pixel, or if you want to send different events to different pixels.

```html
<FacebookPixel bind:this={fb} />

<script>
	import FacebookPixel from '@beyonk/svelte-facebook-pixel'
	import { onMount } from 'svelte
	
	let fb

	onMount(() => {
		fb.track('SomeEvent', { some: 'data' })
	})
</script>

<FacebookPixel ref:fb id={['123', '456']} />

<script>
  import FacebookPixel from '@beyonk/svelte-facebook-pixel'
</script>
```

By default all pixels are initialised with `init()`, and events will be sent to all pixels, however, you can send tracking events to indiviual pixels if you would like:

#### Sending events to all pixels

You can send tracking events to all pixels just as you would with a single pixel:

```js
fb.track('SomeEvent', { some: 'data' })
```

#### Sending events to a single pixel

If you have multiple pixels on your page and want to send an event to only one of them, specify the pixel's id as the last parameter:

```js
fb.track('SomeEvent', { some: 'data' }, '456')
```

## Disabling the pixel (for GDPR)

If you'd like to install the pixel disabled, and enable it later after the user has consented to its use, you can do so by setting `enabled: false` in the pixel configuration:

```html
<FacebookPixel bind:this={fb} enabled={false} />
```

Now, in your component, you can call the following in order to start the pixel and track the current page.

```js
fb.enable()
```

## Module options

List of possible options in the module:

| Option   | Default  | Required | Description                                                                               |
|----------|----------|----------|-------------------------------------------------------------------------------------------|
| id  | null     | true     | The unique pixel identifier provided by Facebook.                                         |
| version  | v3.1     | false    | Tracking version.                                                                         |
| enabled  | true     | false    | Disable the Pixel by default when initialized. Can be enabled later through `<component>.enable()`. |

## License

[MIT License](./LICENSE)

## Thanks

Thanks to [William DASILVA](https://github.com/WilliamDASILVA/nuxt-facebook-pixel-module) for his original Nuxt facebook pixel module which inspired this project.

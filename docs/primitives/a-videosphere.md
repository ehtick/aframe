---
title: <a-videosphere>
type: primitives
layout: docs
parent_section: primitives
source_code: src/extras/primitives/primitives/a-videosphere.js
examples:
  - title: Adding a Videosphere
    src: https://glitch.com/edit/#!/aframe-360-video-example?path=index.html
---

The videosphere primitive plays 360&deg; videos in the background of the scene.
Videospheres are a large sphere with the video texture mapped to the inside.

## Examples

```html
<a-scene>
  <a-assets>
    <video id="antarctica" autoplay loop="true" src="antarctica.mp4"> </video>
  </a-assets>

  <!-- Using the asset management system. -->
  <a-videosphere src="#antarctica"></a-videosphere>

  <!-- Defining the URL inline. Not recommended but more comfortable for web developers. -->
  <a-videosphere src="africa.mp4"></a-videosphere>
</a-scene>
```

## Methods 

More indepth knowledge on the methods to alter video material can be seen over [here](../components/material.md#video-textures)

```javascript
// to set specific time of video
document.querySelector("#antarctica").components.material.data.src.currentTime = 0 // start of video

// to play the videosphere
document.querySelector("#antarctica").components.material.material.map.image.play();
```

## Attributes

| Attribute       | Component Mapping       | Default Value |
|-----------------|-------------------------|---------------|
| autoplay        | `<video>`.autoplay      | true          |
| crossOrigin     | `<video>`.crossOrigin   | anonymous     |
| loop            | `<video>`.loop          | true          |
| radius          | geometry.radius         | 5000          |
| segments-height | geometry.segmentsHeight | 64            |
| segments-width  | geometry.segmentsWidth  | 64            |



## Equirectangular Video

[equirectangular]: https://en.wikipedia.org/wiki/Equirectangular_projection

To be seamless, source videos should be [equirectangular][equirectangular].

## Caveats

iOS has a lot of restrictions on playing videos in the browser. To play an inline video texture, we must:

- Set the `<meta name="apple-mobile-web-app-capable" content="yes">` meta tag. A-Frame will inject this if missing.
- Set the `webkit-playsinline` and `playsinline` attribute to the video element. A-Frame will add this to all videos if missing).
- Pin the webpage to the iOS homescreen.

Inline video support on iOS 10 may change this. On certain Android devices or
browsers, we must:

[android-touch-bug]: https://bugs.chromium.org/p/chromium/issues/detail?id=178297

- Require user interaction to trigger the video (such as a click or tap event). See [Chromium Bug 178297][android-touch-bug]

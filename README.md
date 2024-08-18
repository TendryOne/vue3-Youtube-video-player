# vue3-youtube-video-player

A Vue 3 component for easily integrating YouTube videos into your Vue applications. This component offers customizable options for video playback, including controls, autoplay, and custom play button styling.

## Installation

To install the package, use npm or yarn:

```bash
npm install vue3-youtube-video-player
```
or

```bash
yarn add vue3-youtube-video-player
```

## Usage

Import the Component
In your Vue file, import and register the component:
```vue
<script setup>
import YoutubeVideoPlayer from 'vue3-youtube-video-player';
</script>
```

##Add the Component to Your Template
Use the `<YoutubeVideoPlayer>` component in your template:

``` vue
<template>
  <div>
    <YoutubeVideoPlayer
      videoId="dD7VD9fCRpU"
      :autoplay="true"
      :controls="false"
      :showinfo="true"
      :width="800"
      :height="450"
      colorPlayButton="white"
      backgroundColorPlayButton="black"
      @onEnded="handleVideoEnd"
    />
  </div>
</template>

<script setup>
const handleVideoEnd = () => {
  console.log('Video has ended.');
};
</script>
```
|name | type | description |
|-----------|-----------|-----------|
| videoId  | string   | The YouTube video ID to play |
| width  | number | Valeur 6  |
| Valeur 7  |number | Valeur 9  |
| Valeur 7  | number  | Valeur 9  |
| Valeur 7  |number | Valeur 9  |
| Valeur 7  |number  | Valeur 9  |
| Valeur 7  | string | Valeur 9  |
| Valeur 7  | string  | Valeur 9  |
|showThumbnailOnEnd   | boolean  | Valeur 9  |




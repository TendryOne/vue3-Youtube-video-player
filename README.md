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
## Available Props

|name | type | description |
|-----------|-----------|-----------|
| videoId  | string   | The YouTube video ID to play |
| width  | number | The height of the video player (in pixels). Default value: `500` |
| Valeur 7  |number | The width of the video player (in pixels). Default value: `500`  |
| Valeur 7  | number  |minimizes YouTube branding. Default value: `true` |
| Valeur 7  |number | shows the video controls  |
| Valeur 7  |number  | shows related videos at the end of playback. Default value: `false` |
| Valeur 7  |number  | shows related videos at the end of playback. Default value: `false` |
| Valeur 7  | number | shows video information before playback. Default value: `true` |
| colorPlayButton  | string  | The color of the play button (in CSS format, e.g., white, #000000). Default value: `black`  |
| backgroundColorPlayButton  | string  | The background color of the play button (in CSS format). Default value: `white` |
|showThumbnailOnEnd   | boolean  | to control whether the thumbnail is displayed when the video ends  |

## Events

`onEnded` : Emitted when the video has finished playing. Use this event to trigger additional actions

## Customisation example

``` vue

<template>
  <div>
    <YoutubeVideoPlayer
      videoId="nwpARFlhjXQ"
      :autoplay="true"
      :controls="false"
      :showinfo="true"
      :colorPlayButton="'red'"
      :backgroundColorPlayButton="'yellow'"
    />
  </div>
</template>

```

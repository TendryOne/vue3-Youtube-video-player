<template>
    <div class="video-container" :style="{ width: `${width}px`, height: `${height}px` }">

        <div v-if="showThumbnail" class="thumbnail-container" @click="playVideo">
            <img :src="thumbnailUrl" alt="Video Thumbnail" />

            <button :disabled="!isPlayerReady" class="button-play"
                :style="{ backgroundColor: backgroundColorPlayButton, color: colorPlayButton, position: 'absolute', borderRadius: '100%' }">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="60" height="60">
                    <path d="M8 5v14l11-7z" fill="currentColor" />
                </svg>

            </button>
        </div>
        <div ref="player"></div>
    </div>
</template>

<script setup lang="ts">

import { ref, computed, onMounted } from 'vue';

const props = withDefaults(defineProps<{
    width?: number,
    height?: number,
    videoId?: string,
    controls?: number,
    modestBranding?: number,
    rel?: number,
    showinfo?: number,
    colorPlayButton?: string,
    backgroundColorPlayButton?: string,
    showThumbnailOnEnd?: boolean
}>(), {
    width: 500,
    height: 500,
    controls: 1,
    modestBranding: 1,
    rel: 0,
    showinfo: 0,
    colorPlayButton: 'black',
    backgroundColorPlayButton: 'white',
    showThumbnailOnEnd: true
});

const emit = defineEmits<{
    (e: 'onEnded',): void
}>()


const thumbnailUrl = computed(() => {
    return `https://img.youtube.com/vi/${props.videoId}/maxresdefault.jpg`;
});

const showThumbnail = ref(true);
const isPlayerReady = ref(false);
const player = ref<HTMLDivElement | null>(null);

let ytPlayer: YT.Player;

const loadYouTubeIframeAPI = () => {
    return new Promise<void>((resolve) => {
        if ((window as any).YT && (window as any).YT.Player) {
            resolve();
        } else {
            const script = document.createElement('script');
            script.src = 'https://www.youtube.com/iframe_api';
            script.onload = () => resolve();
            document.body.appendChild(script);
        }
    });
};

const initializePlayer = () => {
    ytPlayer = new (window as any).YT.Player(player.value, {
        height: `100%`,
        width: `100%`,
        videoId: props.videoId,
        playerVars: {
            controls: props.controls,
            modestbranding: props.modestBranding,
            rel: props.rel,
            showinfo: props.showinfo
        },
        events: {
            'onReady': onPlayerReady,
            'onStateChange': onPlayerStateChange
        }
    });
};

const playVideo = () => {
    if (ytPlayer && ytPlayer.playVideo) {
        showThumbnail.value = false;
        ytPlayer.playVideo();
    } else {
        console.error('Player is not ready');
    }
};

const onPlayerReady = (event: YT.PlayerEvent) => {
    isPlayerReady.value = true;
};

const onPlayerStateChange = (event: YT.OnStateChangeEvent) => {
    if (event.data === YT.PlayerState.ENDED) {
        if (props.showThumbnailOnEnd) {
            showThumbnail.value = true;
        }
        emit('onEnded');

    }
};

onMounted(async () => {
    await loadYouTubeIframeAPI();
    if ((window as any).YT && (window as any).YT.Player) {
        initializePlayer();
    } else {
        (window as any).onYouTubeIframeAPIReady = initializePlayer;
    }
});
</script>



<style scoped>
.video-container {
    position: relative;
    width: 100%;
    height: 390px;
}

.thumbnail-container {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: black;
    cursor: pointer;
}



.thumbnail-container img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.play-button {
    position: absolute;
    font-size: 50px;
    color: red;
    border: none;
    cursor: pointer;
    /* background-color: rgb(255, 255, 255); */
    padding: 20px 25px;
    border-radius: 100%;
}

.play-button:disabled {
    background-color: rgba(0, 0, 0, 0.3);
    cursor: not-allowed;
}

.button-play {
    cursor: pointer;
    display: flex;
    width: 70px;
    height: 70px;
    display: flex;
    align-items: center;
    justify-content: center;
}
</style>
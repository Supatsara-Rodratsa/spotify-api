<script setup>
import { computed } from '@vue/runtime-core';
import TrackList from './TrackList.vue';
const props = defineProps({ album: Object, artists: Object });

const totalSong = computed(() => {
    if (props.album.total_tracks == 1) {
        return '1 Song';
    } else {
        return `${props.album.total_tracks} Songs`;
    }
});

const date = computed(() => {
    const tempDate = new Date(props.album.release_date);
    return tempDate.toLocaleDateString("en-US", { year: 'numeric', month: 'short', day: 'numeric' });
});
</script>

<template>
    <div class="flex-row container">
        <div class="details flex-col album-content">
            <div class="header">{{album.name}}</div>
            <div class="contents"><span class="topic">Total Track:</span> {{totalSong}}</div>
            <div class="contents"><span class="topic">Release Date:</span> {{date}}</div>
            <div class="flex-row">
                <div><span class="topic">Artist:</span></div>
                <div v-for="artist in artists" v-bind:key="artist.id">
                    <div class="flex-col center gap">
                        <img :src="artist.image" alt="Avatar">
                        <div class="contents">{{artist.name}}</div>
                    </div>
                </div>
            </div>
        </div>
        <TrackList :path="album.url" class="frame-container"/>
    </div>
</template>

<style scoped>

.container {
    width: 100%;
    margin: 20px 0;
}
.details {
    width: 35%;
    text-align: left;
    color: white;
    font-size: 18px;
}

.frame-container {
    width: 65%;
}

.album-content {
    justify-content: start;
    align-items: flex-start;
}

.header {
    font-weight: 700;
    font-size: 24px;
    margin: 20px 0;
}

.flex-col  {
    gap: 20px;
}

.topic {
    font-size: 18px;
    font-weight: 500;
    margin-right: 10px;
}

img {
    border-radius: 50%;
    width: 75px;
    height: 75px;
  }

.center {
    align-items: center;
    justify-content: center;
}

.gap {
    gap: 10px !important;
}

.contents {
    font-size: 16px;
}
</style>
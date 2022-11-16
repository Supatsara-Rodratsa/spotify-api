<script setup>
import { computed } from "@vue/runtime-core";

const { newAlbum } = defineProps({ newAlbum: Object });

const totalSong = computed(() => {
    if (newAlbum.total_tracks == 1) {
        return '1 Song';
    } else {
        return `${newAlbum.total_tracks} Songs`;
    }
})
</script>
<template>
    <div class="card-container" :style="`background-image: url(${newAlbum.image})`">
        <div class="content-bg flex-col from-bottom">
            <div class="pad-20 gap-5 flex-col algin-start">
                <div class="header title">{{newAlbum.name}}</div>
                <div class="description">{{totalSong}}</div>
            </div>
        </div>
    </div>
    
</template>
<style scoped>
    .card-container {
        width: 250px;
        height: 250px;
        background-repeat: no-repeat;
        background-size: cover;
        border-radius: 8px;
        box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
        cursor: pointer;
    }

    .content-bg:hover {
        background: linear-gradient(rgba(0, 0, 0, 0.2), rgba(128,0,128, 1));
    }

    .content-bg {
        height: 100%;
        width: 100%;
        background: linear-gradient(rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.6));
        color: white;
        border-radius: 8px;
    }

    .pad-20 {
        padding: 20px;
    }

    .gap-5 {
        gap: 5px;
    }

    .algin-start {
        align-items: start;
    }

    .title {
        width: 100%;
        max-height: 45px; 
        overflow: hidden;
        text-overflow: ellipsis; 
        text-align: start;
        display: -webkit-box !important;
        -webkit-line-clamp: 2;
        -webkit-box-orient: vertical;
        white-space: normal;
    }
</style>

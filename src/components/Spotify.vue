<script setup>
import { ref } from 'vue';
import { getToken, getNewRelease } from '../services/spotifyAPI';
import { CONSTANTS } from '../constants/constants';
import Album  from './Album.vue'

const newReleaseData = ref([]);
try {
    const token = await getToken(CONSTANTS.SPOTIFY_CLIENT_ID, CONSTANTS.SPOTIFY_CLIENT_SECRET);
    const response= await getNewRelease(token);
    transformData(response)
} catch(e) {
    throw e;
}

function transformData(albums) {
    if (albums.albums) {
        for (let item of albums.albums.items) {
            newReleaseData.value.push({
                id: item.id,
                album_type: item.album_type,
                artists: item.artists[0],
                url: item.external_urls.spotify,
                image: item.images[0].url,
                name: item.name,
                release_date: item.release_date,
                total_tracks: item.total_tracks
            });
        }
    }
}
</script>
<template>
    <h2 class="flex">New Release</h2>
    <div class="scroll">
        <template class="flex-row">
            <div v-for="item in newReleaseData" v-bind:key="item.id">
                <Album :newAlbum="item"></Album>
            </div>
        </template>
    </div>
</template>
  
<style scoped>
.scroll {
    min-height: 150px;
    padding: 10px;
    overflow-x: scroll;
    overflow-y: hidden;
}
</style>
<script setup>
import { ref } from 'vue';
import { getToken, getNewRelease, getArtistInfo } from '../services/spotifyAPI';
import { CONSTANTS } from '../constants/constants';
import AlbumDetail  from '../components/AlbumDetail.vue';
import Album from './Album.vue';
import LazyLoadDetail from './LazyLoadDetail.vue';
import Error from './Error.vue'

const error = ref(null);
const selectedAlbum = ref(null);
const newReleaseData = ref([]);
const token = ref('');
const artistsInfo = ref([]);
try {
    token.value = await getToken(CONSTANTS.SPOTIFY_CLIENT_ID, CONSTANTS.SPOTIFY_CLIENT_SECRET);
    const response= await getNewRelease(token.value);
    transformData(response);
} catch(err) {
    error.value = err;
    throw err;
}

async function transformData(albums) {
    if (albums.albums) {
        let index = 0;
        for (let item of albums.albums.items) {
            newReleaseData.value.push({
                id: item.id,
                album_type: item.album_type,
                artists: item.artists,
                url: item.external_urls.spotify,
                image: item.images[0].url,
                name: item.name,
                release_date: item.release_date,
                total_tracks: item.total_tracks
            });

            if (index == 0) {
                showDetail(newReleaseData.value[0]);
            }
            index++;
        }
    }
}

async function showDetail(album) {
    try {
        selectedAlbum.value = null;
        artistsInfo.value = [];
        for (let artist of album.artists) {
            const response = await getArtistInfo(token.value, artist.id);
            if (response) {
                artistsInfo.value.push({
                    id: artist.id,
                    name: response.name,
                    image: response.images[0].url,
                });
            }
        }
        await new Promise(resolve => {
            setTimeout(() => {
                selectedAlbum.value = album;
            }, 500)
        });
    } catch(err) {
        error.value = err;
        throw err;
    }
}

</script>
<template>
    <div class="scrolling-wrapper">
        <template class="flex-row">
            <div v-for="item in newReleaseData" v-bind:key="item.id">
                <Album :newAlbum="item" @click="showDetail(item)"></Album>
            </div>
        </template>
    </div>
    <AlbumDetail v-if="selectedAlbum" :album="selectedAlbum" :artists="artistsInfo"></AlbumDetail>
    <LazyLoadDetail v-if="!selectedAlbum && !error"/>
    <Error :error="error" v-if="error"/>
</template>
  
<style scoped>
.container {
    width: 100%;
}
.scrolling-wrapper {
    overflow-x: scroll;
    overflow-y: hidden;
    white-space: nowrap;
    padding-bottom: 60px;
}
Album {
    display: inline-block;
}
</style>
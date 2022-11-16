<script setup>
defineProps({ newAlbum: Object });
</script>
<template>
    <div class="card-container" :style="`background-image: url(${newAlbum.image})`">
        <div class="content-bg flex-col from-bottom">
            <div class="pad-20 gap-5 flex-col algin-start">
                <div class="header">{{newAlbum.name}}</div>
                <div>fds</div>
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
    }

    .content-bg {
        height: 100%;
        width: 100%;
        background-image: linear-gradient(rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.5));
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
</style>

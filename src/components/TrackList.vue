<script setup>
import { computed } from "@vue/runtime-core";
const props = defineProps({ path: String });

const transformEmbed = computed(() => {
    const position = props.path.lastIndexOf("album");
    return props.path.substring(0,position)+"embed/"+props.path.substring(position);
});
</script>

<template>
    <div id="track">
         <div class="container">
            <iframe class="frame" loading="lazy" :src="transformEmbed" allow="encrypted-media;autoplay; fullscreen" ></iframe>
        </div>
    </div>
</template>

<style scoped>
    .container {
        left: 0; 
        width: 100%; 
        height: 380px; 
        position: relative;
    }

    .frame {
        top: 0; 
        left: 0; 
        width: 100%; 
        height: 100%; 
        position: absolute; 
        border: 0;
        border-radius: 8px;
    }
</style>
<template>
    <div class="flex-row container">
        <div class="flex-col gap-10 detail-container">
            <div class="details"></div>
            <div class="content-1"></div>
            <div class="content-2"></div>
        </div>
        <div class="frame-container"></div>
    </div>
</template>
<style scoped>
.container {
    width: 100%;
    margin: 20px 0;
}

.detail-container {
    width: 40%;
}
.details {
    width: 100%;
    height: 200px;
    text-align: left;
    color: white;
    font-size: 18px;
    animation: loadingColor 1s linear infinite alternate;
    border-radius: 8px;
}

.frame-container {
    width: 60%;
    animation: loadingColor 1s linear infinite alternate;
    border-radius: 8px;
}

.gap-10 {
    gap: 10px;
}

.content-1 {
    width: 200px;
    height: 10px;
    background-color: lightgray;
    animation: loadingColor 1s linear infinite alternate;
}

.content-2 {
    width: 150px;
    height: 10px;
    background-color: lightgray;
    animation: loadingColor 1s linear infinite alternate;
}

</style>
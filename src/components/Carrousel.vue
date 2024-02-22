<template>
    <div class="image-carousel">
    <img :src="currentImage" alt="Carousel Image" />
        <div class = 'General-Carrousel'>
            <div v-for="(image, index) in images" :key="index" class="dot" :class="{ 'active-dot': index === currentIndex }" @click="changeImage(index)">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 16 16" fill="none">
                <circle cx="8" cy="8" r="8" :fill="index === currentIndex ? '#EF8354' : '#DDE1E4'" />
            </svg>
        </div>
    </div>
</div>
</template>

<script setup>

import { ref, onMounted } from 'vue';
const images = [
    'https://iili.io/JIhJ9Hv.png',
    'https://iili.io/JIhJSzN.png',
    'https://iili.io/JIhJvbp.png',
];
const currentIndex = ref(0);
const currentImage = ref(images[currentIndex.value]);

const startCarousel = () => {
    setInterval(() => {
        nextImage();
    }, 5000);
};
const nextImage = () => {
    currentIndex.value = (currentIndex.value + 1) % images.length;
    currentImage.value = images[currentIndex.value];
};
const changeImage = (index) => {
    currentIndex.value = index;
    currentImage.value = images[currentIndex.value];
};
onMounted(() => {
    startCarousel();
});

</script>


<style scoped>
.image-carousel {
    position: relative;
}
.image-carousel img {
    width: 241px;
    height: 216px;
    object-fit: contain;
}
.General-Carrousel{
    display: flex;
    justify-content: center;
}
.dot {
    width: 16px;
    height: 16px;
    display: inline-block;
    margin: 0 5px;
    cursor: pointer;
}
</style>

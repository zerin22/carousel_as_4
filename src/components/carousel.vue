<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const items = [
    {
        image: "/images/img1.jpg",
        caption: "Image 1"
    },
    {
        image: "/images/img4.jpg",
        caption: "Image 2"
    },
    {
        image: "/images/img4cafe.jpg",
        caption: "Image 3"
    }
];

const activeImage = ref(0);
let duration = null;

const incrementImageValue = () => {
    if (activeImage.value == items.length - 1) {
        activeImage.value = 0
    }
    else {
        activeImage.value++
    }
}


const startSlide = function () {
    duration = setInterval(incrementImageValue, 2000)
}

const stopSlide = function () {
    clearInterval(duration)
}

onMounted(() => {
    startSlide()
})

onUnmounted(() => {
    stopSlide()
})
</script>

<template>
    <h2 class="text-center text-secondary">Slider Here</h2>
    <div @mouseover="stopSlide" @mouseleave="startSlide" id="carouselExampleCaptions" class="carousel">
        <ol class="carousel-indicators">
            <li @click="activeImage = index" v-for="(item, index) in items" :key="index"
                :class="index == activeImage ? 'active' : ''"></li>
        </ol>

        <div class="carousel-inner">
            <div class="carousel-item active">
                <img :src="items[activeImage].image" class="d-block w-100 img img-responsive" alt="...">
                <div class="carousel-caption d-none d-md-block">
                    <p> {{ items[activeImage].caption }}</p>
                </div>
            </div>
        </div>
        <a @click.prevent="0 == activeImage ? activeImage = (items.length) - 1 : activeImage--"
            class="carousel-control-prev" href="#" role="button">
            <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        </a>
        <a @click.prevent="(items.length) - 1 == activeImage ? activeImage = 0 : activeImage++"
            class="carousel-control-next" href="#" role="button">
            <span class="carousel-control-next-icon" aria-hidden="true"></span>
        </a>
    </div>
</template>

<style scoped>
.carousel-inner {
    width: 800px;
    height: 500px;
}
</style>

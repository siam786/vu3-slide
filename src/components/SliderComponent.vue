<template>
  <div class="carousel">
    <transition name="carousel-fade">
      <div class="carousel-inner">
        <div v-for="(item, index) in carouselItems" :key="index" :class="['carousel-item', index === activeIndex ? 'active' : '']">
          <img :src="item.image" class="d-block w-100" alt="Slide Image" v-show="isActiveSlide(index)">
          <div class="carousel-caption d-none d-md-block">
            <h5>{{ item.title }}</h5>
            <p>{{ item.caption }}</p>
          </div>
        </div>
      </div>
    </transition>

    <a class="carousel-control-prev" href="#" role="button" @click="prevSlide">
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="visually-hidden">Previous</span>
    </a>
    <a class="carousel-control-next" href="#" role="button" @click="nextSlide">
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="visually-hidden">Next</span>
    </a>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const activeIndex = ref(0);
const autoplayInterval = ref(null);

const carouselItems = [
  {
    image: 'https://images.pexels.com/photos/376464/pexels-photo-376464.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    title: 'First Slide',
    caption: 'Nulla vitae elit libero, a pharetra augue mollis interdum.',
  },
  {
    image: 'https://images.pexels.com/photos/1640774/pexels-photo-1640774.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    title: 'Second Slide',
    caption: 'Nulla vitae elit libero, a pharetra augue mollis interdum.',
  },
  {
    image: 'https://images.pexels.com/photos/1775043/pexels-photo-1775043.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    title: 'Third Slide',
    caption: 'Nulla vitae elit libero, a pharetra augue mollis interdum.',
  },
];

const prevSlide = () => {
  activeIndex.value = (activeIndex.value - 1 + carouselItems.length) % carouselItems.length;
};

const nextSlide = () => {
  activeIndex.value = (activeIndex.value + 1) % carouselItems.length;
};

const isActiveSlide = (index) => {
  return index === activeIndex.value;
};

onMounted(() => {
  // Start autoplay when component is mounted
  startAutoplay();
});

onUnmounted(() => {
  // Stop autoplay when component is unmounted
  stopAutoplay();
});

const startAutoplay = () => {
  autoplayInterval.value = setInterval(() => {
    nextSlide();
  }, 5000); // Change slide every 3 seconds (adjust as needed)
};

const stopAutoplay = () => {
  clearInterval(autoplayInterval.value);
};


</script>

<style scoped>
.carousel {
  position: relative;
}

.carousel-inner {
  overflow: hidden;
}

.carousel-item {
  display: none;
}

.carousel-item.active {
  display: block;
}

.carousel-caption {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 15px;
  background: rgba(0, 0, 0, 0.6);
  color: #fff;
}

.carousel-control-prev,
.carousel-control-next {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 3rem;
  height: 3rem;
  font-size: 2rem;
  color: #fff;
  background: rgba(0, 0, 0, 0.6);
  border: none;
  border-radius: 50%;
  z-index: 10;
  cursor: pointer;
}

.carousel-control-prev {
  left: 1rem;
}

.carousel-control-next {
  right: 1rem;
}

/* Fade-in and fade-out effect during transition */
.carousel-fade-enter-active,
.carousel-fade-leave-active {
  transition: opacity 1s;
}

.carousel-fade-enter,
.carousel-fade-leave-to /* .carousel-fade-leave-active in <2.1.8 */ {
  opacity: 0;
}
</style>

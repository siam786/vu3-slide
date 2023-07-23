<template>
  <div class="carousel">
    <h3 class="fs-1 text-gr mb-4 fw-bold text-uppercase">{{ title }}</h3>
    <TransitionGroup  name="carousel-fade">
      <div class="carousel-inner rounded ">
        <div v-for="(item, index) in carouselItems" :key="index" :class="['carousel-item', index === activeIndex ? 'active' : '']" class="image-slider">
          <img :src="item.image" class="img-fluid img-rounded shadow-4-strong d-block w-100" alt="Slide Image" v-show="isActiveSlide(index)">
          <div class="carousel-caption d-none d-md-block">
            <h5>{{ item.title }}</h5>
            <p>{{ item.caption }}</p>
          </div>
        </div>
      </div>
    </TransitionGroup >

    <a class="carousel-control-prev" href="#" role="button" @click="prevSlide">
      <!-- <span class="carousel-control-prev-icon" aria-hidden="true"></span> -->
      <i class="fa-solid fa-arrow-left" style="color: #ededed;"></i>
    </a>
    <a class="carousel-control-next" href="#" role="button" @click="nextSlide">
      <!-- <span class="carousel-control-next-icon" aria-hidden="true"></span> -->
      <i class="fa-solid fa-arrow-right" style="color: #ededed;"></i>
    </a>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const activeIndex = ref(0);
const autoplayInterval = ref(null);
const title='Vue 3 Slider'
let carouselItems = [
  {
    image: 'https://images.pexels.com/photos/2865987/pexels-photo-2865987.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    title: 'Refreshing Watermelon',
    caption: 'A juicy watermelon slice, perfect for summer.',
  },
  {
    image: 'https://images.pexels.com/photos/4022107/pexels-photo-4022107.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    title: 'Vibrant Orange',
    caption: 'A ripe orange with a burst of vitamin C.',
  },
  {
    image: 'https://images.pexels.com/photos/7195273/pexels-photo-7195273.jpeg?auto=compress&cs=tinysrgb&w=1260',
    title: 'Exotic Pineapple',
    caption: 'A tropical pineapple that transports you to an island getaway.',
  },
  {
    image: 'https://images.pexels.com/photos/3085062/pexels-photo-3085062.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    title: 'Sweet Grapes',
    caption: 'A bunch of juicy grapes, nature\'s candy.',
  },
  {
    image: 'https://images.pexels.com/photos/1128678/pexels-photo-1128678.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    title: 'Juicy Berries',
    caption: 'A mix of delicious berries full of antioxidants.',
  },
  {
    image: 'https://images.pexels.com/photos/8523860/pexels-photo-8523860.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    title: 'Tropical Mango',
    caption: 'A ripe mango, the king of fruits in the tropics.',
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
  }, 3000); // Change slide every 3 seconds (adjust as needed)
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
.text-gr{
  background: #F85032;
background: -webkit-repeating-radial-gradient(circle farthest-corner at bottom right, #F85032 16%, #F16F5C 42%, #F6290C 51%, #F02F17 65%, #E73827 100%);
background: -moz-repeating-radial-gradient(circle farthest-corner at bottom right, #F85032 16%, #F16F5C 42%, #F6290C 51%, #F02F17 65%, #E73827 100%);
background: repeating-radial-gradient(circle farthest-corner at bottom right, #F85032 16%, #F16F5C 42%, #F6290C 51%, #F02F17 65%, #E73827 100%);
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;

}


.image-slider img:first-child {
  opacity: 1; /* Show the first image initially */
}

@keyframes slide {
	0% {
		animation-timing-function: ease-in;
		opacity: 1;
		transform: translateY(45px);
	}

	24% {
		opacity: 1;
	}

	40% {
		animation-timing-function: ease-in;
		transform: translateY(24px);
	}

	65% {
		animation-timing-function: ease-in;
		transform: translateY(12px);
	}

	82% {
		animation-timing-function: ease-in;
		transform: translateY(6px);
	}

	93% {
		animation-timing-function: ease-in;
		transform: translateY(4px);
	}

	25%,
	55%,
	75%,
	87% {
		animation-timing-function: ease-out;
		transform: translateY(0px);
	}

	100% {
		animation-timing-function: ease-out;
		opacity: 1;
		transform: translateY(0px);
	}
}
.image-slider {
  /* animation: slide 9s infinite linear; Adjust the animation duration */
  animation: slide 2s ease-out 0s 1 normal both;
}
</style>

<template>
    <div class="carousel" tabindex="0" @keydown="handleKeyDown"  @focus="stopAutoRotate" @blur="startAutoRotate">
      <div class="slides" :style="{ transform: 'translateX(' + (-currentIndex * 100) + '%)' }">
        <div class="slide" v-for="(slide, index) in slides" :key="index" :aria-hidden="index !== currentIndex">
          <img :src="slide.image" :alt="slide.alt">
          <p>{{ slide.caption }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        currentIndex: 0,
        slides: [
          { image: './assets/image/image1.png', alt: 'Image 1', caption: 'Image description 1' },
          { image: './assets/image/image1.png', alt: 'Image 2', caption: 'Image description 2' },
          { image: './assets/image/image1.png', alt: 'Image 3', caption: 'Image description 3' },
          { image: './assets/image/image1.png', alt: 'Image 4', caption: 'Image description 4' },
          { image: './assets/image/image1.png', alt: 'Image 5', caption: 'Image description 5' }
        ],
        intervalId: null
      };
    },
    mounted() {
      this.startAutoRotate();
    },
    methods: {
      toggleAutoRotate() {
        this.autoRotate = !this.autoRotate;
        if (this.autoRotate) {
            this.startAutoRotate();
        } else {
            this.stopAutoRotate();
        }
      },
      handleKeyDown(event) {
        if (event.key === 'ArrowRight') {
          this.nextSlide();
        } else if (event.key === 'ArrowLeft') {
          this.prevSlide();
        }
      },
      startAutoRotate() {
        this.intervalId = setInterval(this.nextSlide, 3000); // Rotate every 3 seconds
      },
      stopAutoRotate() {
        clearInterval(this.intervalId);
      },
      nextSlide() {
        this.currentIndex = (this.currentIndex + 1) % this.slides.length;
      },
      prevSlide() {
        this.currentIndex = (this.currentIndex - 1 + this.slides.length) % this.slides.length;
      }
    },
    beforeUnmount() {
      this.stopAutoRotate();
    }
  };
  </script>
  
  <style scoped>
  .carousel {
    position: relative;
    overflow: hidden;
    width: 100%;
    height: 300px; /* Adjust height as needed */
  }
  
  .slides {
    display: flex;
    transition: transform 0.5s ease;
  }
  
  .slide {
    flex: 0 0 100%;
  }
  
  .slide img {
    width: 100%;
    height: auto;
  }
  
  /* .slide p {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    color: #fff;
    padding: 10px;
    margin: 0;
  } */
  </style>
  
<template>
    <div class="carousel-wrapper">
      <div class="carousel" >
        <div class="slides" :aria-live="autoRotate? 'off' : 'polite'"  @focus="stopAutoRotate" @blur="startAutoRotate" :style="{ transform: 'translateX(' + (-currentIndex * 100) + '%)' }">
          <figure v-for="(slide, index) in slides" :key="index"
            :tabindex="index === currentIndex ? 0 : -1" 
            role="group" 
            aria-roledescription="slide" 
            class="slide"  
            :aria-hidden="index !== currentIndex" >
            <img :src="slide.image" :alt="slide.alt">
            <figcaption>{{ slide.caption }}</figcaption>
          </figure>
        </div>
      </div>
      <button @click="toggleAutoRotate" class="control-btn" :aria-label="autoRotate ? 'Stop' : 'Start'" >{{ autoRotate ? 'Stop' : 'Start' }}</button>
      <button class="previous round" aria-label="previous" @click="prevSlide1">&#8249;</button>
      <button class="next round" aria-label="next" @click="nextSlide1">&#8250;</button>
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
        autoRotate: true,
        intervalId: null
      };
    },
    mounted() {
      this.startAutoRotate();
    },
    methods: {
      startAutoRotate() {
        this.intervalId = setInterval(this.nextSlide, 3000); // Rotate every 3 seconds
      },
      stopAutoRotate() {
        clearInterval(this.intervalId);
      },
      nextSlide() {
        if (this.autoRotate) {
          this.currentIndex = (this.currentIndex + 1) % this.slides.length;
        }
      },
        nextSlide1() {
          if (!this.autoRotate) {
          this.currentIndex = (this.currentIndex + 1) % this.slides.length;
        }
       },
      prevSlide() {
        if (this.autoRotate){
          this.currentIndex = (this.currentIndex - 1 + this.slides.length) % this.slides.length;
        }
      },
      prevSlide1() {
        if (!this.autoRotate) {
          this.currentIndex = (this.currentIndex - 1 + this.slides.length) % this.slides.length;
        }
      },
      toggleAutoRotate() {
        this.autoRotate = !this.autoRotate;
        if (this.autoRotate) {
          this.startAutoRotate();
        } else {
          this.stopAutoRotate();
        }
      }
    },
    beforeUnmount() {
      this.stopAutoRotate();
    }
  };
  </script>
  
  <style scoped>
  .carousel-wrapper {
    position: relative;
  }
  
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
  
  .control-btn {
    position: absolute;
    bottom: 10px;
    left: 10px;
    padding: 5px 10px;
    background-color: #333;
    color: #fff;
    border: none;
    cursor: pointer;
    outline-offset: 2px;
    border-radius: 25%;
    
  }
  button {
  text-decoration: none;
  display: inline-block;
  padding: 8px 16px;
  outline-offset: 1px;
  }
  button:hover {
  background-color: black;
  color: #f1f1f1;
}

.previous {
  background-color: #f1f1f1;
  color: black;
}

.next {
  background-color: #f1f1f1;
  color: black;
}

.round {
  border-radius: 50%;
}
  </style>
  
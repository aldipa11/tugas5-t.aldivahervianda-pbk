<template>
    <q-carousel
      v-model="slide"
      navigation
      swipeable
      animated
      infinite
      thumbnails
      :arrows="false"
      class="bg-grey-2 text-black"
    >
      <q-carousel-slide
        v-for="(image, index) in images"
        :key="index"
        :name="index"
        :img-src="image"
      />
    </q-carousel>
  </template>
  
  <script>
  export default {
    name: 'Carousel',
    data() {
      return {
        slide: 0,
        images: [
          'https://via.placeholder.com/1200x400?text=Slide+1',
          'https://via.placeholder.com/1200x400?text=Slide+2',
          'https://via.placeholder.com/1200x400?text=Slide+3'
        ]
      };
    }
  };
  </script>
  
<template>
  <flickity class="banner" ref="flickity" :options="flickityOptions">
    <div class="carousel-cell0"></div>
    <div class="carousel-cell1"></div>
  </flickity>
</template>

<script>
import Flickity from 'vue-flickity';
export default {
  name: 'HomeView',
  components: {
    Flickity
   },
  data() {
    return {
      flickityOptions: {
        autoPlay: 3000,
        pageDots: true,
        resize: true,
        prevNextButtons: true,
        wrapAround: true
      }
    }
  },
  methods: {
    next() {
      this.$refs.flickity.next();
    },
    
    previous() {
      this.$refs.flickity.previous();
    }
  }
}
</script>

<style scoped>
.banner {
  width: 100%;
  height: 100%;
  background-color: rgb(18, 21, 25);
}
.carousel-cell {
  width: 100%;
  height: 100%;
}
.carousel-cell0 {
  width: 100%;
  height: 100%;
  background-image:url("https://massyule.com/img/banner2.cc360d91.png");
  background-repeat: no-repeat;
  background-position: center;
}
.carousel-cell1 {
  width: 100%;
  height: 100%;
  background-image:url("https://massyule.com/img/banner.7bd43ead.jpg");
  background-repeat: no-repeat;
  background-position: center;
}
</style>
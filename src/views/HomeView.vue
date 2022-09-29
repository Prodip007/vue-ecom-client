<template>
  <div class="home">
    <div class="slider">
      <h1>My Slider</h1>
      <div class="slide">
        <img src="@/assets/clue-avenue-escape-rooms.jpg" alt="" />
        <h3>Slide 1</h3>
      </div>
      <div class="slide">
        <img src="@/assets/Hero-Image-3.png" alt="" />
        <h3>Slide 2</h3>
      </div>
      <div class="slide">
        <img src="@/assets/home-page-cover.png" alt="" />
        <h3>Slide 3</h3>
      </div>
      <a class="navigation prev" @click="changeSlide(-1)">&#10094;</a>
      <a class="navigation next" @click="changeSlide(1)">&#10095;</a>
    </div>

    <div class="newswipwer-slider">
      <swiper :slides-per-view="3" :space-between="50" @swiper="onSwiper" @slideChange="onSlideChange">
        <swiper-slide class="my-swslide">
          <div class="hero-body has-text-centered">
            <p class="title mb-6">Welcome to Django-Vue Ecom</p>
            <p class="subtitle">The best jacket store online</p>
          </div>
          Slide 1
        </swiper-slide>
        <swiper-slide class="my-swslide">
          <div class="hero-body has-text-centered">
            <p class="title mb-6">Welcome to Django-Vue Ecom</p>
            <p class="subtitle">The best jacket store online</p>
          </div>
          Slide 2
        </swiper-slide>
        <swiper-slide class="my-swslide">
          Slide 3
          <div class="hero-body has-text-centered">
            <p class="title mb-6">Welcome to Django-Vue Ecom</p>
            <p class="subtitle">The best jacket store online</p>
          </div>
        </swiper-slide>
        <swiper-slide class="my-swslide">
          Slide 4
          <div class="hero-body has-text-centered">
            <p class="title mb-6">Welcome to Django-Vue Ecom</p>
            <p class="subtitle">The best jacket store online</p>
          </div>
        </swiper-slide>
        <swiper-slide class="my-swslide">
          Slide 5
          <div class="hero-body has-text-centered">
            <p class="title mb-6">Welcome to Django-Vue Ecom</p>
            <p class="subtitle">The best jacket store online</p>
          </div>
        </swiper-slide>
        <swiper-slide class="my-swslide">
          Slide 6
          <div class="hero-body has-text-centered">
            <p class="title mb-6">Welcome to Django-Vue Ecom</p>
            <p class="subtitle">The best jacket store online</p>
          </div>
        </swiper-slide>
        <swiper-slide class="my-swslide">
          Slide 7
          <div class="hero-body has-text-centered">
            <p class="title mb-6">Welcome to Django-Vue Ecom</p>
            <p class="subtitle">The best jacket store online</p>
          </div>
        </swiper-slide>
        <swiper-slide class="my-swslide">
          Slide 8
          <div class="hero-body has-text-centered">
            <p class="title mb-6">Welcome to Django-Vue Ecom</p>
            <p class="subtitle">The best jacket store online</p>
          </div>
        </swiper-slide>
        <swiper-slide class="my-swslide">
          Slide 9
          <div class="hero-body has-text-centered">
            <p class="title mb-6">Welcome to Django-Vue Ecom</p>
            <p class="subtitle">The best jacket store online</p>
          </div>
        </swiper-slide>
        ...
      </swiper>
    </div>

    <section class="hero is-medium is-dark mb-6">
      <div class="hero-body has-text-centered">
        <p class="title mb-6">Welcome to Django-Vue Ecom</p>
        <p class="subtitle">The best jacket store online</p>
      </div>
    </section>

    <div class="column is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centered">Latest products</h2>
      </div>
      <div class="columns">
        <product-box v-for="product in latestProducts" :key="product.id" :product="product" />
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css";

import axios from "axios";
import ProductBox from "@/components/ProductBox.vue";

export default {
  name: "Home",

  data() {
    return {
      latestProducts: [],
      slideIndex: 0,
    };
  },

  components: {
    ProductBox,
    Swiper,
    SwiperSlide,
  },

  setup() {
    const onSwiper = (swiper) => {
      console.log(swiper);
    };
    const onSlideChange = () => {
      console.log("slide change");
    };
    return {
      onSwiper,
      onSlideChange,
    };
  },

  mounted() {
    this.getLatestProducts();
    document.title = "Home | VEcom";
  },
  methods: {
    async getLatestProducts() {
      this.$store.commit("setIsLoading", true);
      await axios
        .get("/api/v1/latest-products/")
        .then((response) => {
          this.latestProducts = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
      this.$store.commit("setIsLoading", false);
    },

    showSlides(n) {
      let slides = document.getElementsByClassName("slide");
      let localIndex = n;
      if (localIndex < 0) {
        localIndex = slides.length - 1;
        this.slideIndex = localIndex;
      } else if (localIndex > slides.length - 1) {
        localIndex = 0;
        this.slideIndex = localIndex;
      }
      for (let i = 0; i < slides.length; i++) {
        slides[i].style.display = "none";
      }
      slides[localIndex].style.display = "block";
      console.log(localIndex);
    },

    changeSlide(n) {
      let newIndex = this.slideIndex + n;
      this.slideIndex = newIndex;
      this.showSlides(newIndex);
    },
  },
  mounted() {
    this.showSlides(this.slideIndex);
  },
};
</script>

<style src="@/assets/css/style.css"></style>

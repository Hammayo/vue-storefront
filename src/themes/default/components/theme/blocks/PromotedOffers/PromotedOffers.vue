<template>
  <section v-if="!singleBanner" class="offers container my30">
    <div class="row m0">
      <div
        class="offer-container col-xs-12 col-sm-6 px15"
        v-for="(banner, index) in banners.mainBanners"
        :key="index"
      >
        <router-link :to="banner.link">
          <div
            class="offer border-box p5 flex center-xs middle-xs cl-white bg-cl-th-accent"
            v-lazy:background-image="banner.image"
          >
            <p class="subtitle m0 serif h3 uppercase">
              {{ banner.subtitle }}
            </p>
            <h2 class="title m0 h1">
              {{ banner.title }}
            </h2>
          </div>
        </router-link>
      </div>

      <div class="col-xs-12 col-sm-6 p0">
        <div
          class="offer-container px15 pb30"
          v-for="(banner, index) in banners.smallBanners"
          :key="index"
        >
          <router-link :to="banner.link">
            <div
              class="offer offer-small border-box p5 flex center-xs middle-xs cl-white bg-cl-th-accent"
              v-lazy:background-image="banner.image"
            >
              <p class="subtitle m0 serif h3 uppercase">{{ banner.subtitle }}</p>
              <h2 class="title m0 h1">{{ banner.title }}</h2>
            </div>
          </router-link>
        </div>
      </div>
    </div>
  </section>
  <section v-else class="container my30">
    <div
      class="col-xs-12 px15"
      v-for="(banner, index) in banners.productBanners"
      :key="index"
    >
      <router-link :to="banner.link">
        <div
          class="offer offer-product border-box p5 flex center-xs middle-xs cl-white bg-cl-th-accent"
          v-lazy:background-image="banner.image"
        >
          <p class="subtitle m0 serif h3 uppercase">
            {{ banner.subtitle }}
          </p>
          <h2 class="title m0 h1">
            {{ banner.title }}
          </h2>
        </div>
      </router-link>
    </div>
  </section>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
import promotedOffers from 'theme/resource/promoted_offers.json'

export default {
  name: 'PromotedOffers',
  created () {
    this.updatePromotedOffers(promotedOffers)
  },
  props: {
    singleBanner: {
      type: Boolean,
      required: false,
      default: false
    }
  },
  computed: {
    ...mapGetters({
      banners: 'promoted/getPromotedOffers'
    })
  },
  methods: {
    ...mapActions({
      updatePromotedOffers: 'promoted/updatePromotedOffers'
    })
  }
}
</script>

<style lang="scss" scoped>
 .offers {
    @media (max-width: 767px) {
      padding: 0 15px;
    }
  }
  .offer-container {
    &:last-child {
      padding-bottom: 0;
    }

    @media (max-width: 767px) {
      padding: 5px 0;
    }
  }
  .offer {
    height: 750px;
    flex-direction: column;
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
    opacity: 0.9;
    transition: 0.3s all;

    &:hover {
      opacity: 1;
    }

    @media (max-width: 767px) {
      height: 200px;
    }
  }
  .offer-small {
    height: 360px;

    @media (max-width: 767px) {
      height: 200px;
    }
  }
  .offer-product {
    height: 330px;
    background-position: 50% 20%;

    @media (max-width: 767px) {
      height: 330px;
    }
  }
  .title {
    @media (max-width: 767px) {
      font-size: 36px;
    }
  }
  .subtitle {
    @media (max-width: 767px) {
      font-size: 18px;
    }
  }
</style>

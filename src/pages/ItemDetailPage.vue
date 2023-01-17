<template>
  <q-page v-if="item" padding>
    <q-btn flat color="primary" label="ATRAS" to="/" />
    <div class="row">
      <div class="col-12 col-md-6 col-lg-4">
        <q-carousel
          v-model="slide"
          transition-prev="jump-right"
          transition-next="jump-left"
          swipeable
          infinite
          animated
          control-color="white"
          prev-icon="arrow_left"
          next-icon="arrow_right"
          navigation-icon="radio_button_unchecked"
          navigation
          padding
          arrows
          height="300px"
          class="bg-purple text-white shadow-1 rounded-borders"
        >
          <q-carousel-slide name="style" class="column no-wrap flex-center">
            <q-icon name="style" size="56px" />
            <div class="q-mt-md text-center">
              Lorem ipsum dolor sit amet, consectetur adipiscing elit
            </div>
          </q-carousel-slide>
          <q-carousel-slide name="tv" class="column no-wrap flex-center">
            <q-icon name="live_tv" size="56px" />
            <div class="q-mt-md text-center">
              Lorem ipsum dolor sit amet, consectetur adipiscing elit
            </div>
          </q-carousel-slide>
        </q-carousel>
      </div>
      <div class="col-12 col-md-6 col-lg-8">
        <q-card class="my-card" flat>
          <q-card-section>
            <div class="text-h6">{{ item.name }}</div>
            <div class="text-subtitle2">by John Doe</div>
          </q-card-section>
          <q-card-section>
            {{ item.description }}
          </q-card-section>
          <q-card-section>
            <div class="row">
              <div class="col-6">RD$ XX.XX</div>
              <div class="col-6">
                <q-btn color="primary" label="Solicitar" @click="openLink" />
              </div>
            </div>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </q-page>
  <q-page v-else>
    <q-inner-loading showing>
      <q-spinner-gears size="50px" color="primary" />
    </q-inner-loading>
  </q-page>
</template>

<script>
import { openURL } from "quasar";
export default {
  // name: 'PageName',
  data() {
    return {
      slide: "tv",
      item: null,
    };
  },
  computed: {
    id() {
      return this.$route.params.id;
    },
  },
  methods: {
    getItemDetails() {
      this.$api.get(`items/${this.id}/`).then((response) => {
        this.item = response.data;
      });
    },
    openLink() {
      openURL(
        "https://wa.me/18295480472?text=Hola! me interesaria adquirir 'Hola man'"
      );
    },
  },
  mounted() {
    this.getItemDetails();
  },
};
</script>

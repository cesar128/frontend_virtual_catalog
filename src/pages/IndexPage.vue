<template>
  <q-page v-if="items" class="" padding>
    <div class="row q-col-gutter-lg">
      <div
        class="col-12 col-md-4 col-xl-3"
        v-for="item in items"
        :key="item.id"
      >
        <q-card class="my-card">
          <img src="https://cdn.quasar.dev/img/mountains.jpg" />
          <q-card-section>
            <div class="text-h6">{{ item.name }}</div>
            <div class="text-subtitle2"></div>
          </q-card-section>
          <q-card-section>
            {{ item.description }}
          </q-card-section>
          <q-card-section>
            <q-btn color="primary" label="Detalles" :to="'/' + item.id" />
          </q-card-section>
        </q-card>
      </div>
    </div>
  </q-page>
  <q-page v-else class="flex flex-center">
    <q-spinner-dots color="primary" size="3rem" :thickness="5" />
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import { openURL } from "quasar";

export default defineComponent({
  name: "IndexPage",

  data() {
    return {
      items: null,
    };
  },

  methods: {
    getItems() {
      this.$api.get("items/").then((response) => {
        this.items = response.data;
      });
    },
    selectItem(product_name) {},
  },
  mounted() {
    this.getItems();
  },
});
</script>

<template>
  <transition-group
    name="fade"
    tag="div"
    @beforeEnter="before"
    @enter="enter"
    @leave="leave"
  >
    <div
      class="row d-none mb-3 align-items-center border-bottom p-2"
      v-for="(item, index) in showItem"
      :key="item.id"
      :data-index="index"
    >
      <div class="col-1 m-auto">
        <button
          class="btn btn-info text-light fw-bold"
          @click="$emit('add-item', item)"
        >
          +
        </button>
      </div>
      <div class="col-4">
        <img :src="item.image" :alt="item.name" class="img-fluid d-block" />
      </div>
      <div class="col">
        <h3 class="text-info">{{ item.name }}</h3>
        <p class="mb-0 text-start">{{ item.description }}</p>
        <div class="h5 float-end">
          <price :value="Number(item.price)"></price>
        </div>
      </div>
    </div>
  </transition-group>
</template>

<script>
import Price from "./Price.vue";

export default {
  name: "product-list",
  components: {
    Price,
  },
  props: ["products", "maximum"],
  computed: {
    showItem: function () {
      let max = this.maximum;
      return this.products.filter(function (item) {
        return item.price <= max;
      });
    },
  },
  methods: {
    before: function (el) {
      el.className = "d-none";
    },
    enter: function (el) {
      var delay = el.dataset.index * 100;
      setTimeout(function () {
        el.className =
          "row d-flex mb-3 align-items-center animate__animated animate__fadeInRight";
      }, delay);
    },
    leave: function (el) {
      var delay = el.dataset.index * 100;
      setTimeout(function () {
        el.className =
          "row d-flex mb-3 align-items-center animate__animated animate__fadeOutRight";
      }, delay);
    },
  },
};
</script>

<template>
  <div>
    <h1>IDShop</h1>
    <navbar
      :cart="cart"
      :cartQty="cartQty"
      :cartTotal="cartTotal"
      @toggle-slider="toggleSlider"
      @delete-item="deleteItem"
    ></navbar>
    <price-slider
      :sliderStatus="sliderStatus"
      :maximum.sync="maximum"
    ></price-slider>
    <product-list
      :products="products"
      :maximum="maximum"
      @add-item="addItem"
    ></product-list>
  </div>
</template>

<script>
import Navbar from "./Navbar.vue";
import ProductList from "./ProductList.vue";
import PriceSlider from "./PriceSlider.vue";

export default {
  name: "products",
  props: [
    "products",
    "maximum",
    "cart",
    "cartQty",
    "cartTotal",
    "sliderStatus",
    "sliderState",
  ],
  components: {
    Navbar,
    PriceSlider,
    ProductList,
  },
  methods: {
    toggleSlider: function () {
      this.$emit("toggle-slider");
    },
    addItem: function (item) {
      this.$emit("add-item", item);
    },
    deleteItem: function (index) {
      this.$emit("delete-item", index);
    },
  },
};
</script>

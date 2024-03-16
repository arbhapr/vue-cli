<template>
  <nav class="navbar navbar-light fixed-top">
    <div class="navbar-text ms-auto pe-3 d-flex">
      <button
        class="btn btn-sm btn-outline-success"
        @click="$emit('toggle-slider')"
      >
        <font-awesome-icon icon="dollar-sign"></font-awesome-icon>
      </button>
      <div class="ms-2" v-if="cart.length > 0">
        <button
          class="btn btn-success btn-sm dropdown-toggle"
          id="dropdownCart"
          data-bs-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          <span class="badge badge-pill text-bg-success">
            {{ cartQty }}
          </span>
          <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
          <price :value="Number(cartTotal)"></price>
        </button>
        <div
          class="dropdown-menu dropdown-menu-end"
          aria-labelledby="dropdownCart"
        >
          <div v-for="(item, index) in cart" :key="index">
            <div class="dropdown-item-text text-nowrap text-end">
              <span
                class="badge badge-pill text-bg-warning align-text-top me-1"
              >
                {{ item.qty }}
              </span>
              {{ item.product.name }}
              <b>
                {{ (item.product.price * item.qty) | currencyFormat }}
              </b>
              <a
                href="#"
                class="badge text-bg-danger text-white text-decoration-none"
                @click.stop="$emit('delete-item', index)"
              >
                -
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import Price from "./Price.vue";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

export default {
  components: {
    Price,
    FontAwesomeIcon,
  },
  props: ["cart", "cartQty", "cartTotal"],
  filters: {
    currencyFormat: function (value) {
      return "Rp" + Number.parseFloat(value).toFixed(2);
    },
  },
};
</script>

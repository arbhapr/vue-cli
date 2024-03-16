<template>
  <transition
    name="custom"
    enter-active-class="animate__animated animate__fadeInDown"
    leave-active-class="animate__animated animate__slideOutRight"
  >
    <div class="" v-if="sliderStatus">
      <div class="row align-items-center pb-3" :class="sliderState">
        <label for="" class="font-weight-bold me-2">Max</label>
        <input
          type="number"
          class="col-2 form-control"
          style="width: 70px; text-align: center"
          id=""
          v-model="maxAmount"
          @change="$emit('update:maximum', maxAmount)"
        />
        <input
          type="range"
          name=""
          id=""
          class="col ps-3 form-range"
          min="0"
          max="150"
          v-model="maxAmount"
          @input="$emit('update:maximum', maxAmount)"
        />
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "price-slider",
  data: function () {
    return {
      maxAmount: 50,
    };
  },
  props: ["sliderStatus", "maximum"],
  computed: {
    sliderState: function () {
      return this.sliderStatus ? "d-flex" : "d-none";
    },
  },
};
</script>

<style>
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 3s ease-in-out;
}
</style>

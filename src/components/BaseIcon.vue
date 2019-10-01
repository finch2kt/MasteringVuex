<template>
  <div class="icon-wrapper">
    <svg class="icon" :width="width" :hieght="hieght">
      <use v-bind="{ 'xlink:href': '/feather-sprite.svg#' + name }" />
    </svg>
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: {
    name: String,
    width: {
      type: [Number, String],
      default: 24
    },
    hieght: {
      type: [Number, String],
      default: 24
    }
  }
};
</script>

<style scoped></style>

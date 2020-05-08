<template>
  <v-btn
    height="35"
    :width="width"
    depressed
    small
    tile
    color="white"
    :ripple="ripple"
  >
    <span
      v-if="!center"
      class="d-inline-block text-truncate text-left"
      style="width: 180px;"
    >
      {{ value }}
    </span>
    <span v-else>
      {{ value }}
    </span>
  </v-btn>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: undefined
    },
    center: {
      type: Boolean,
      default: false
    },
    ripple: {
      type: Boolean,
      default: false
    },
    width: {
      type: Number,
      default: 200
    }
  }
}
</script>

<style scoped></style>

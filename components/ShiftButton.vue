<template>
  <v-btn
    height="35px"
    width="35px"
    rounded
    depressed
    small
    :color="color"
    :ripple="false"
    >{{ shift }}</v-btn
  >
</template>

<script>
export default {
  props: {
    schedule: {
      type: Number,
      default: undefined
    },
    additional: {
      type: Number,
      default: undefined
    },
    active: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    shift() {
      const id = this.schedule

      if (id === undefined) return

      return this.$store.state.shift.find(
        (s) => parseInt(s.id) === parseInt(id)
      ).kode
    },
    color() {
      if (this.active) {
        return 'grey lighten-2'
      }
      if (this.additional) {
        return this.$store.getters.color(this.additional)
      }
      return 'white'
    }
  }
}
</script>

<style scoped></style>

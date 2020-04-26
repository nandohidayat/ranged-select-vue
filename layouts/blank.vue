<template>
  <v-app class="gradient">
    <v-content>
      <v-container class="fill-height">
        <nuxt />
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {}
</script>

<style scoped>
.gradient {
  background: rgb(255, 255, 255);
  background: radial-gradient(
    circle,
    rgba(255, 255, 255, 1) 0%,
    rgba(234, 234, 245, 1) 100%,
    rgba(238, 249, 251, 1) 100%
  );
}
</style>

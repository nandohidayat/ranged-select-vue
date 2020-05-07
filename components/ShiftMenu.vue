<template>
  <v-menu
    v-model="menu"
    :position-x="x"
    :position-y="y"
    absolute
    offset-y
    :close-on-click="false"
    :close-on-content-click="false"
    z-index="13"
  >
    <v-list>
      <div v-if="switches">
        <v-list-item
          v-for="(j, i) in fJob"
          :key="i"
          @click="updateSchedule(j.id, 'additional')"
        >
          <v-list-item-title>{{ j.job }}</v-list-item-title>
        </v-list-item>
      </div>
      <div v-else>
        <v-list-item
          v-for="(s, i) in fShift"
          :key="i"
          @click="updateSchedule(s.id)"
        >
          <v-list-item-title>{{ s.kode }}</v-list-item-title>
        </v-list-item>
      </div>
      <v-list-item @click="reset()"
        ><v-icon color="error">mdi-close</v-icon></v-list-item
      >
    </v-list>
  </v-menu>
</template>

<script>
export default {
  props: {
    staff: {
      type: Number,
      default: undefined
    },
    day: {
      type: Array,
      default: () => []
    },
    switches: {
      type: Boolean,
      default: false
    },
    menu: {
      type: Boolean,
      default: false
    },
    x: {
      type: Number,
      default: 0
    },
    y: {
      type: Number,
      default: 0
    }
  },
  computed: {
    fShift() {
      return [{ id: undefined, kode: undefined }, ...this.$store.state.shift]
    },
    fJob() {
      return [
        { id: undefined, job: undefined, color: 'white' },
        ...this.$store.state.job
      ]
    }
  },
  methods: {
    updateSchedule(value, type = 'schedule') {
      this.$store.commit('updateSchedule', {
        staff: this.staff,
        day: this.day,
        value,
        type
      })
      this.reset()
    },
    reset() {
      this.$emit('update:menu', false)
      this.$emit('update:staff', undefined)
      this.$emit('update:day', [])
    }
  }
}
</script>

<style scoped></style>

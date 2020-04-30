<template>
  <v-card
    max-height="400px"
    style="overflow-y: auto; overflow-x: auto; white-space: nowrap;"
  >
    <div
      :style="{
        zIndex: 10,
        position: 'sticky',
        backgroundColor: 'white',
        left: 0
      }"
      class="shadow d-inline-block"
    >
      <div :style="{ position: 'sticky', top: 0, zIndex: 11 }" class="shadow">
        <v-btn height="40" width="200" depressed small tile color="white">
          Nama
        </v-btn>
        <v-divider></v-divider>
      </div>
      <div v-for="(n, i) in $store.state.name" :key="i">
        <v-btn
          height="40"
          width="200"
          depressed
          small
          tile
          color="white"
          @click="nameClick(i)"
          @click.stop="showMenu"
        >
          <span
            class="d-inline-block text-truncate text-left"
            style="width: 180px;"
          >
            {{ n }}
          </span>
        </v-btn>
        <v-divider></v-divider>
      </div>
    </div>
    <div class="d-inline-block">
      <div :style="{ position: 'sticky', top: 0, zIndex: 9 }" class="shadow">
        <span v-for="d in $store.state.day" :key="d">
          <v-btn
            height="40px"
            width="40px"
            tile
            depressed
            small
            :color="dayColor(d)"
            >{{ d }}</v-btn
          >
        </span>
        <v-divider></v-divider>
      </div>
      <div v-for="(schedule, i) in $store.state.schedule" :key="i">
        <span v-for="(s, j) in schedule" :key="j">
          <v-btn
            height="40px"
            width="40px"
            rounded
            depressed
            small
            :color="active(j, i) ? 'grey lighten-2' : 'white'"
            @click="ranged(j, i)"
            @click.stop="showMenu"
            >{{ displayShift(s) }}</v-btn
          >
        </span>
        <v-divider></v-divider>
      </div>
    </div>
    <v-menu
      v-model="menu"
      :position-x="x"
      :position-y="y"
      absolute
      offset-y
      :close-on-click="false"
      :close-on-content-click="false"
      z-index="13"
      @keypress.delete="menu = false"
    >
      <v-list>
        <v-list-item
          v-for="(s, i) in fShift"
          :key="i"
          @click="updateSchedule(s.id)"
        >
          <v-list-item-title>{{ s.kode }}</v-list-item-title>
        </v-list-item>
        <v-list-item @click="reset()"
          ><v-icon color="error">mdi-close</v-icon></v-list-item
        >
      </v-list>
    </v-menu>
  </v-card>
</template>

<script>
export default {
  layout: 'blank',
  data() {
    return {
      day: [],
      staff: undefined,
      menu: false,
      x: 0,
      y: 0
    }
  },
  computed: {
    fShift() {
      return [{ id: undefined, kode: undefined }, ...this.$store.state.shift]
    }
  },
  methods: {
    ranged(day, staff) {
      if (
        this.day.length === 0 ||
        this.day.length === 2 ||
        this.staff !== staff
      ) {
        this.staff = staff
        this.day = [day]
      } else if (this.day[0] < day) {
        this.day.push(day)
      } else if (this.day[0] > day) {
        this.day.unshift(day)
      } else {
        this.staff = undefined
        this.day = []
      }
    },
    active(day, staff) {
      if (
        this.staff === staff &&
        (day === this.day[0] || (day > this.day[0] && day <= this.day[1]))
      ) {
        return true
      }
      return false
    },
    nameClick(staff) {
      if (this.staff !== undefined && this.staff === staff) {
        this.day = []
        this.staff = undefined
      } else {
        this.staff = staff
        this.day = [0, this.$store.state.day - 1]
      }
    },
    showMenu(e) {
      if (this.staff === undefined) return (this.menu = false)
      this.menu = true
      this.x = e.clientX
      this.y = e.clientY
    },
    updateSchedule(s) {
      this.$store.commit('updateSchedule', {
        staff: this.staff,
        day: this.day,
        shift: s
      })
      this.reset()
    },
    reset() {
      this.menu = false
      this.staff = undefined
      this.day = []
    },
    displayShift(id) {
      if (id === undefined) return
      return this.$store.state.shift.find(
        (s) => parseInt(s.id) === parseInt(id)
      ).kode
    },
    dayColor(d) {
      if (this.$store.state.weekend.includes(d)) return 'red'
      if (this.$store.state.holiday.includes(d)) return 'red lighten-3'
      return 'white'
    }
  }
}
</script>

<style scoped>
.shadow {
  -webkit-box-shadow: 4px 0px 5px 0px rgba(0, 0, 0, 0.27);
  -moz-box-shadow: 4px 0px 5px 0px rgba(0, 0, 0, 0.27);
  box-shadow: 4px 0px 5px 0px rgba(0, 0, 0, 0.27);
}
</style>

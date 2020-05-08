<template>
  <v-card raised>
    <div
      style="overflow-y: auto; overflow-x: auto; white-space: nowrap;max-height: 450px"
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
          <v-btn height="35" width="200" depressed small tile color="white">
            Nama
          </v-btn>
          <v-divider></v-divider>
        </div>
        <div v-for="(n, i) in $store.state.name" :key="i">
          <view-button
            :value="n"
            @click.native="nameClick(i)"
            @click.native.stop="showMenu"
          ></view-button>
          <v-divider></v-divider>
        </div>
      </div>
      <div class="d-inline-block">
        <div :style="{ position: 'sticky', top: 0, zIndex: 9 }" class="shadow">
          <v-btn
            v-for="d in $store.state.day"
            :key="d"
            height="35px"
            width="35px"
            tile
            depressed
            small
            :color="$store.getters.dayColor(d)"
            >{{ d }}</v-btn
          >
          <v-divider></v-divider>
        </div>
        <div v-for="(schedule, i) in $store.state.schedule" :key="i">
          <shift-button
            v-for="(s, j) in schedule"
            :key="j"
            :schedule="s"
            :additional="$store.state.additional[i][j]"
            :active="active(j, i)"
            @click.native="ranged(j, i)"
            @click.native.stop="showMenu"
          ></shift-button>
          <v-divider></v-divider>
        </div>
      </div>
      <div class="d-inline-block">
        <div :style="{ position: 'sticky', top: 0, zIndex: 9 }" class="shadow">
          <v-btn height="35" width="120" depressed small tile color="white">
            Total Jam
          </v-btn>
          <v-divider></v-divider>
        </div>
        <div v-for="(jam, i) in $store.state.jam" :key="i">
          <v-btn
            height="35"
            width="120"
            depressed
            small
            tile
            color="white"
            :ripple="false"
          >
            {{ jam }}
          </v-btn>
          <v-divider></v-divider>
        </div>
      </div>
      <shift-menu
        :staff.sync="staff"
        :day.sync="day"
        :menu.sync="menu"
        :switches="switches"
        :x="x"
        :y="y"
      ></shift-menu>
    </div>
    <v-row style="height: 40px" no-gutters align="center" justify="end">
      <v-switch
        v-model="switches"
        inset
        class="ma-0 pa-0 mr-4"
        :hide-details="true"
        color="teal"
        label="Jobs"
        dense
      ></v-switch>
    </v-row>
    <v-divider></v-divider>
    <div class="text-center">
      source code :
      <a href="https://github.com/nandohidayat/ranged-select-vue"
        >https://github.com/nandohidayat/ranged-select-vue</a
      >
    </div>
  </v-card>
</template>

<script>
import ShiftButton from '@/components/ShiftButton'
import ShiftMenu from '@/components/ShiftMenu'
import ViewButton from '@/components/ViewButton'

export default {
  layout: 'blank',
  components: {
    ShiftButton,
    ShiftMenu,
    ViewButton
  },
  data() {
    return {
      day: [],
      staff: undefined,
      menu: false,
      x: 0,
      y: 0,
      switches: false
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
      if (this.staff === staff) {
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

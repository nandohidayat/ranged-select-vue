<template>
  <v-card raised>
    <div
      style="overflow-y: auto; overflow-x: auto; white-space: nowrap;max-height: 500px"
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
        <div>
          <div v-for="(n, i) in name1" :key="i">
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
        <div v-if="$store.state.name.length > 5">
          <div v-for="(n, i) in name2" :key="i">
            <v-btn
              height="40"
              width="200"
              depressed
              small
              tile
              color="white"
              @click="nameClick(i + 5)"
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
        <div v-if="$store.state.name.length > 10">
          <div v-for="(n, i) in name3" :key="i">
            <v-btn
              height="40"
              width="200"
              depressed
              small
              tile
              color="white"
              @click="nameClick(i + 10)"
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
        <div v-if="$store.state.name.length > 15">
          <div v-for="(n, i) in name4" :key="i">
            <v-btn
              height="40"
              width="200"
              depressed
              small
              tile
              color="white"
              @click="nameClick(i + 15)"
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
        <div v-if="$store.state.name.length > 20">
          <div v-for="(n, i) in name5" :key="i">
            <v-btn
              height="40"
              width="200"
              depressed
              small
              tile
              color="white"
              @click="nameClick(i + 20)"
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
        <div v-if="$store.state.name.length > 25">
          <div v-for="(n, i) in name6" :key="i">
            <v-btn
              height="40"
              width="200"
              depressed
              small
              tile
              color="white"
              @click="nameClick(i + 25)"
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
        <div v-if="$store.state.name.length > 30">
          <div v-for="(n, i) in name7" :key="i">
            <v-btn
              height="40"
              width="200"
              depressed
              small
              tile
              color="white"
              @click="nameClick(i + 30)"
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
        <div v-if="$store.state.name.length > 35">
          <div v-for="(n, i) in name8" :key="i">
            <v-btn
              height="40"
              width="200"
              depressed
              small
              tile
              color="white"
              @click="nameClick(i + 35)"
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
        <div>
          <div v-for="(schedule, i) in schedule1" :key="i">
            <span v-for="(s, j) in schedule" :key="j">
              <v-btn
                height="40px"
                width="40px"
                rounded
                depressed
                small
                :color="
                  active(j, i)
                    ? 'grey lighten-2'
                    : displayJob($store.state.extra[i][j])
                "
                @click="ranged(j, i)"
                @click.stop="showMenu"
                >{{ displayShift(s) }}</v-btn
              >
            </span>
            <v-divider></v-divider>
          </div>
        </div>
        <div v-if="$store.state.schedule.length > 5">
          <div v-for="(schedule, i) in schedule2" :key="i">
            <span v-for="(s, j) in schedule" :key="j">
              <v-btn
                height="40px"
                width="40px"
                rounded
                depressed
                small
                :color="
                  active(j, i + 5)
                    ? 'grey lighten-2'
                    : displayJob($store.state.extra[i + 5][j])
                "
                @click="ranged(j, i + 5)"
                @click.stop="showMenu"
                >{{ displayShift(s) }}</v-btn
              >
            </span>
            <v-divider></v-divider>
          </div>
        </div>
        <div v-if="$store.state.schedule.length > 10">
          <div v-for="(schedule, i) in schedule3" :key="i">
            <span v-for="(s, j) in schedule" :key="j">
              <v-btn
                height="40px"
                width="40px"
                rounded
                depressed
                small
                :color="
                  active(j, i + 10)
                    ? 'grey lighten-2'
                    : displayJob($store.state.extra[i + 10][j])
                "
                @click="ranged(j, i + 10)"
                @click.stop="showMenu"
                >{{ displayShift(s) }}</v-btn
              >
            </span>
            <v-divider></v-divider>
          </div>
        </div>
        <div v-if="$store.state.schedule.length > 15">
          <div v-for="(schedule, i) in schedule4" :key="i">
            <span v-for="(s, j) in schedule" :key="j">
              <v-btn
                height="40px"
                width="40px"
                rounded
                depressed
                small
                :color="
                  active(j, i + 15)
                    ? 'grey lighten-2'
                    : displayJob($store.state.extra[i + 15][j])
                "
                @click="ranged(j, i + 15)"
                @click.stop="showMenu"
                >{{ displayShift(s) }}</v-btn
              >
            </span>
            <v-divider></v-divider>
          </div>
        </div>
        <div v-if="$store.state.schedule.length > 20">
          <div v-for="(schedule, i) in schedule5" :key="i">
            <span v-for="(s, j) in schedule" :key="j">
              <v-btn
                height="40px"
                width="40px"
                rounded
                depressed
                small
                :color="
                  active(j, i + 20)
                    ? 'grey lighten-2'
                    : displayJob($store.state.extra[i + 20][j])
                "
                @click="ranged(j, i + 20)"
                @click.stop="showMenu"
                >{{ displayShift(s) }}</v-btn
              >
            </span>
            <v-divider></v-divider>
          </div>
        </div>
        <div v-if="$store.state.schedule.length > 25">
          <div v-for="(schedule, i) in schedule6" :key="i">
            <span v-for="(s, j) in schedule" :key="j">
              <v-btn
                height="40px"
                width="40px"
                rounded
                depressed
                small
                :color="
                  active(j, i + 25)
                    ? 'grey lighten-2'
                    : displayJob($store.state.extra[i + 25][j])
                "
                @click="ranged(j, i + 25)"
                @click.stop="showMenu"
                >{{ displayShift(s) }}</v-btn
              >
            </span>
            <v-divider></v-divider>
          </div>
        </div>
        <div v-if="$store.state.schedule.length > 30">
          <div v-for="(schedule, i) in schedule7" :key="i">
            <span v-for="(s, j) in schedule" :key="j">
              <v-btn
                height="40px"
                width="40px"
                rounded
                depressed
                small
                :color="
                  active(j, i + 30)
                    ? 'grey lighten-2'
                    : displayJob($store.state.extra[i + 30][j])
                "
                @click="ranged(j, i + 30)"
                @click.stop="showMenu"
                >{{ displayShift(s) }}</v-btn
              >
            </span>
            <v-divider></v-divider>
          </div>
        </div>
        <div v-if="$store.state.schedule.length > 35">
          <div v-for="(schedule, i) in schedule8" :key="i">
            <span v-for="(s, j) in schedule" :key="j">
              <v-btn
                height="40px"
                width="40px"
                rounded
                depressed
                small
                :color="
                  active(j, i + 35)
                    ? 'grey lighten-2'
                    : displayJob($store.state.extra[i + 35][j])
                "
                @click="ranged(j, i + 35)"
                @click.stop="showMenu"
                >{{ displayShift(s) }}</v-btn
              >
            </span>
            <v-divider></v-divider>
          </div>
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
      >
        <v-list>
          <div v-if="switches">
            <v-list-item
              v-for="(j, i) in fJob"
              :key="i"
              @click="updateSchedule(j.id, 'extra')"
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
    </div>
    <v-row style="height: 50px" no-gutters align="center" justify="end">
      <v-switch
        v-model="switches"
        inset
        class="ma-0 pa-0 mr-4"
        :hide-details="true"
        color="teal"
        label="Jobs"
      ></v-switch>
    </v-row>
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
      y: 0,
      switches: false
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
    },
    name1() {
      return this.$store.state.name.slice(0, 5)
    },
    name2() {
      return this.$store.state.name.slice(5, 10)
    },
    name3() {
      return this.$store.state.name.slice(10, 15)
    },
    name4() {
      return this.$store.state.name.slice(15, 20)
    },
    name5() {
      return this.$store.state.name.slice(20, 25)
    },
    name6() {
      return this.$store.state.name.slice(25, 30)
    },
    name7() {
      return this.$store.state.name.slice(30, 35)
    },
    name8() {
      return this.$store.state.name.slice(35, 40)
    },
    schedule1() {
      return this.$store.state.schedule.slice(0, 5)
    },
    schedule2() {
      return this.$store.state.schedule.slice(5, 10)
    },
    schedule3() {
      return this.$store.state.schedule.slice(10, 15)
    },
    schedule4() {
      return this.$store.state.schedule.slice(15, 20)
    },
    schedule5() {
      return this.$store.state.schedule.slice(20, 25)
    },
    schedule6() {
      return this.$store.state.schedule.slice(25, 30)
    },
    schedule7() {
      return this.$store.state.schedule.slice(30, 35)
    },
    schedule8() {
      return this.$store.state.schedule.slice(35, 40)
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
    displayJob(id) {
      if (id === undefined) return 'white'
      return this.$store.state.job.find((j) => parseInt(j.id) === parseInt(id))
        .color
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

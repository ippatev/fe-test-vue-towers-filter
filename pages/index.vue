<template>
  <v-row justify="start" align="center">
    <div style="display: block; width: 100%">
      <v-row>
        <v-col>
          <p class="filter--text">КОМНАТЫ</p>
          <v-btn-toggle v-model="filter.rooms" color="primary">
            <v-btn height="40px" rounded class="ms-1 me-1" v-for="(room, idx) of rooms" :key="idx">
              {{ room }}
            </v-btn>
          </v-btn-toggle>
        </v-col>
        <v-col>
          <p class="filter--text">ЭТАЖ</p>
          <div style="width: 175px">
            <v-row>
              <v-col
                class="pt-0"
                cols="12"
                md="6"
              >
                <v-text-field hide-details outlined dense v-model="floor[0]">
                </v-text-field>
              </v-col>
              <v-col
                class="pt-0"
                cols="12"
                md="6"
              >
                <v-text-field hide-details outlined dense v-model="floor[1]">
                </v-text-field>
              </v-col>
            </v-row>
          </div>
          <vue-slider style="width: 175px" color="primary" :max="100" v-model="floor"></vue-slider>
        </v-col>
        <v-col>
          <p class="filter--text">ПЛОЩАДЬ, м<sup>2</sup></p>
          <div style="width: 175px">
            <v-row>
              <v-col
                class="pt-0"
                cols="12"
                md="6"
              >
                <v-text-field hide-details outlined dense v-model="square[0]">
                </v-text-field>
              </v-col>
              <v-col
                class="pt-0"
                cols="12"
                md="6"
              >
                <v-text-field hide-details outlined dense v-model="square[1]">
                </v-text-field>
              </v-col>
            </v-row>
          </div>
          <vue-slider style="width: 175px" color="primary" :max="100" :min="0" v-model="square"></vue-slider>
        </v-col>
        <v-col>
          <p class="filter--text">СТОИМОСТЬ, млн. р.</p>
          <div style="width: 175px">
            <v-row>
              <v-col
                class="pt-0"
                cols="12"
                md="6"
              >
                <v-text-field hide-details outlined dense v-model="sum[0]">
                </v-text-field>
              </v-col>
              <v-col
                class="pt-0"
                cols="12"
                md="6"
              >
                <v-text-field hide-details outlined dense v-model="sum[1]">
                </v-text-field>
              </v-col>
            </v-row>
          </div>
          <vue-slider style="width: 175px" color="primary" :max="100" v-model="sum"></vue-slider>
        </v-col>
        <v-col align-self="center">
          <v-btn @click="onFilter()" elevation="0" width="201px" color="primary" class="text-center mb-2">Применить</v-btn>
          <v-btn @click="onFilter('clear')" width="201px" text class="text-center" elevation="0">сбросить фильтр</v-btn>
        </v-col>
      </v-row>
    </div>
    <card class="mt-8" v-for="(item, idx) in items" :key="idx" :floor="item['floor']" :meter="item.square" :no="item.building_id" :room="item.rooms" :sum="item.price_real" :sub-sum="item.price_real"></card>
  </v-row>
</template>

<script>
import 'vue-slider-component/theme/antd.css'
import json from '~/assets/test-data.json'
import Card from '~/components/Card'

export default {
  components: {
    Card,
  },
  data() {
    return {
      filter: {
        rooms: 1,
        floor: null,
        sum: null,
        square: null
      },
      rooms: [
        'S', '1к', '2к', '3к'
      ],
      floor: [
        '1', '99'
      ],
      sum: [
        '0', '99.9'
      ],
      square: [
        '0', '99.9'
      ],
      items: json
    }
  },
  computed: {
    floorResult(){
      return this.floor[1] - this.floor[0]
    }
  },
  methods: {
    async onFilter(clear) {
      if (clear) {
        this.filter.rooms = 1
        this.floor = [
          '1', '99'
        ]
        this.sum = [
          '0', '99.9'
        ]
        this.square = [
          '0', '99.9'
        ]
        return this.items = json
      }

      const million = 1000000
      let result = []

      // По комнатам
      result = await json.filter(item => item.rooms === this.filter.rooms )

      // По этожу
      result = await result.filter(item => item.floor > parseInt(this.floor[0]))
      result = await result.filter(item => item.floor < parseInt(this.floor[1]))

      // По площади
      result = await result.filter(item => item.square > parseInt(this.square[0]))
      result = await result.filter(item => item.square < parseInt(this.square[1]))

      console.log(parseInt(this.square[0]), parseInt(this.square[1]))

      // По стоимости
      result = await result.filter(item => item.price_real > parseInt(this.sum[0]) * million)
      result = await result.filter(item => item.price_real < parseInt(this.sum[1]) * million)

      console.log(parseInt(this.sum[0]) * million,parseInt(this.sum[1]) * million,)

      this.items = result
    }
  }
}
</script>

<style lang="scss">
$themeColor: #70D24E;

/* import theme style */
@import '~vue-slider-component/lib/theme/default.scss';
  .filter--text {
    font-size: 12px;
    line-height: 20px;
    font-weight: 700;
  }
</style>

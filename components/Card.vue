<template>
  <v-col xl="3" sm="6" cols="12" md="4">
    <v-hover
      v-slot="{ hover }"
      open-delay="200"
    >
      <v-card
        flat
        :class="hover ? 'h-card' : 'card'"
        width="270px"
        height="365px"
        style="text-align: end"
        rounded
      >
        <v-card-actions class="justify-space-between" style="padding: 8px 20px">
          <h4 class="toolbar--text" style="color: rgba(0,0,0,.5)">{{ floor }} этаж</h4>
          <span></span>
          <span></span>
          <h4 class="toolbar--text">{{ room }} комната</h4>
          <span>-</span>
          <h4 class="toolbar--text">{{meter}}м</h4>
        </v-card-actions>
        <div :class="hover ? 'img--small' : 'img--big'">
          <span class="img--text">№{{no}}</span>
          <img
            :src="require('~/assets/card-img.png')"
          />
        </div>

        <v-card-title class="card--title" style="display: block">
          {{sum}}р.
        </v-card-title>

        <v-card-subtitle class="card-subtitle">
          119 000 р. за м<sup><small>2</small></sup>
        </v-card-subtitle>

        <v-card-actions>
          <v-btn
            v-if="hover"
            elevation="0"
            class="white--text"
            block
            color="#70D24E"
          >
            Подробнее
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-hover>
  </v-col>
</template>

<script>
export default {
  name: "Card",
  data() {
    return {
      btnShow: false
    }
  },
  props: {
    floor: {
      type: Number
    },
    room: {
      type: Number
    },
    meter: {
      type: Number
    },
    no: {
      type: Number
    },
    sum: {
      type: Number
    },
    subSum: {
      type: Number
    }
  },
  methods: {
    showButton() {
      this.btnShow = !this.btnShow
    }
  }
}
</script>

<style scoped>

  .card {
    box-shadow: 0px 5px 20px rgba(86, 86, 86, 0.10) !important;
  }

  .h-card {
    box-shadow: 0px 5px 20px rgba(86, 86, 86, 0.25) !important;
  }

  .card--title {
    font-size: 20px;
    font-weight: bold;
    padding-top: 10px;
  }

  .card-subtitle {
    font-size: 12px;
    padding-bottom: 10px;
  }

  .img--big {
    display: flex;
    margin: 0 10px;
    justify-content: center;
    align-items: center;
    border-radius: 5px;
    width: 250px;
    height: 250px;
    border: 1px solid #EBEBEB;
    position: relative;
  }

  .img--small {
    display: flex;
    margin: 0 10px;
    justify-content: center;
    align-items: center;
    border-radius: 5px;
    width: 250px;
    height: 200px;
    border: 1px solid #EBEBEB;
    position: relative;
  }

  .toolbar--text {
    font-weight: 700;
    font-size: 12px;
  }

  .img--text {
    position: absolute;
    right: 0;
    top: 0;
    padding: 4px 10px;
    background-color: white;
    border-left: 1px solid #EBEBEB;
    border-bottom: 1px solid #EBEBEB;
    border-radius: 0px 5px;
    font-size: 14px;
    font-weight: 700;
  }
</style>

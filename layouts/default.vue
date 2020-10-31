<template>
  <v-app dar>
    <h1 class="title">{{ title }}</h1>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-footer
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      title: 'Lorem ipsum dolor sit'
    }
  }
}
</script>

<style scoped>
  .title {
    margin: 38px auto;
    color: #2C323;
    text-align: center;
    font-weight: 700; text-transform: uppercase; font-size: 34px;
  }
</style>

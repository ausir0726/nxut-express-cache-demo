<template>
  <section class="container">
    <div>
      <h1 class="title">
        NUXT
      </h1>
      <h2 v-if="loading" class="subtitle">
        We are fetching latest data. please wait 3 sec ...
      </h2>
      <h2 v-else class="subtitle">
        {{ text }}
      </h2>
      <h4>
        {{ date }}
      </h4>
      <div class="links">
        <a href="https://nuxtjs.org/" target="_blank" class="button--green">Documentation</a>
        <a href="https://github.com/nuxt/nuxt.js" target="_blank" class="button--grey">Github</a>
      </div>
    </div>
  </section>
</template>

<script>
import axios from 'axios'

async function fetchData() {
  const { data } = await axios.get('https://ausir.stdlib.com/vue-test@0.0.0/')
  return Object.assign(data, { date: Date.now() })
}

export default {
  name: 'home',
  data() {
    return { loading: false }
  },
  async asyncData () {
    // get a just 3 second delay api
    return await fetchData();
  },
  async beforeMount () {
    this.loading = true;
    const data = await fetchData();
    this.text = data.text;
    this.date = data.date;
    this.loading = false;
  }
}
</script>

<style>
.container
{
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.title
{
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}
.subtitle
{
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}
.links
{
  padding-top: 15px;
}
</style>

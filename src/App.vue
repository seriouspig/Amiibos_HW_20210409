<template>
  <div id="app">
    <h1>AMIIBOS</h1>
    <amiibos-list :amiibos="amiibos"></amiibos-list>
  </div>
</template>

<script>
import AmiibosList from './components/AmiibosList.vue'

export default {
  name: 'App',
  data() {
    return {
      amiibos: []
    }
  },
  components: {
    'amiibos-list': AmiibosList
  },
  async mounted() {
    const res = await fetch('https://www.amiiboapi.com/api/amiibo/')
    const data = await res.json()
    this.amiibos = data.amiibo
    const uniqueSeries = [...new Set(this.amiibos.map(item => item.amiiboSeries))]
    console.log(uniqueSeries)
    // const uniqueCharacter = [...new Set(this.amiibos.map(item => item.character))]
    // console.log(uniqueCharacter)
    // const uniqueName = [...new Set(this.amiibos.map(item => item.name))]
    // console.log(uniqueName)
    const uniqueType = [...new Set(this.amiibos.map(item => item.type))]
    console.log(uniqueType)
    console.log(this.amiibos[603].name)

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

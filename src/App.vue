<template>
  <div id="app">
    <h1>AMIIBOS</h1>
    <filter-button v-for="(serie, index) in series" :serie="serie" :key="index"
    :amiibos="amiibos" 
    :series="series[index]"></filter-button>
    <amiibos-list :amiibos="filteredAmiibos"></amiibos-list>
  </div>
</template>

<script>
import {eventBus} from './main.js'

import AmiibosList from './components/AmiibosList.vue'
import SeriesFilter from './components/SeriesFilter.vue'

export default {
  name: 'App',
  data() {
    return {
      amiibos: [],
      series: [],
      filteredAmiibos: []
 

    }
  },
  components: {
    'amiibos-list': AmiibosList,
    'filter-button': SeriesFilter
  },
  async mounted() {
    const res = await fetch('https://www.amiiboapi.com/api/amiibo/')
    const data = await res.json()
    this.amiibos = data.amiibo

    this.filteredAmiibos = this.amiibos

    const uniqueSeries = [...new Set(this.amiibos.map(item => item.amiiboSeries))]
    uniqueSeries.unshift("ALL")
    this.series = uniqueSeries
    console.log(uniqueSeries)
    // const uniqueCharacter = [...new Set(this.amiibos.map(item => item.character))]
    // console.log(uniqueCharacter)
    // const uniqueName = [...new Set(this.amiibos.map(item => item.name))]
    // console.log(uniqueName)
    const uniqueType = [...new Set(this.amiibos.map(item => item.type))]
    console.log(uniqueType)
    console.log(this.amiibos[603].name)

    eventBus.$on('series-selected', (series) => {
      if (series==="ALL") {
        this.filteredAmiibos = this.amiibos
      }
      else {
        this.filterAmiibos(series)
      }
      
      console.log(this.filteredAmiibos)
    })
  },
  methods: {
    filterAmiibos(series) {
      const newAmibos = this.amiibos.filter(function(item) {
        return item.amiiboSeries === series 
      })
      this.filteredAmiibos = newAmibos
  }
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

<template>
  <div id="app">
    <div id="grid-container">
      <div id="title">
        <img src="./assets/logo.jpg" alt="amiibos_logo" id="image_logo">
      </div>
      <div id="filters">
        <filter-button v-for="(serie, index) in seriesImgLinks" :serie="serie" :key="index"
        :amiibos="amiibos" 
        :series="series[index]"></filter-button>
      </div>
      
      <div id="list-container">
        
          
              <amiibos-list id="list" :amiibos="filteredAmiibos">
                  

              </amiibos-list>
              <div id="bg">
                <img src="./assets/background.jpg" alt="amiibos_logo">
              </div>
        
        <amiibo-details  id="details" v-if="selectedAmiibo" :selectedAmiibo="selectedAmiibo"></amiibo-details>
      </div>
    </div>
  </div>
</template>

<script>
import {eventBus} from './main.js'

import AmiibosList from './components/AmiibosList.vue'
import SeriesFilter from './components/SeriesFilter.vue'
import AmiiboDetails from './components/AmiiboDetails.vue'

export default {
  name: 'App',
  data() {
    return {
      amiibos: [],
      seriesImgLinks: [],
      series: [],
      filteredAmiibos: [],
      selectedAmiibo: null
 

    }
  },
  components: {
    'amiibos-list': AmiibosList,
    'filter-button': SeriesFilter,
    'amiibo-details': AmiiboDetails

  },
  async mounted() {
    const res = await fetch('https://www.amiiboapi.com/api/amiibo/')
    const data = await res.json()
    this.amiibos = data.amiibo

    this.filteredAmiibos = this.amiibos

    const uniqueSeries = [...new Set(this.amiibos.map(item => item.amiiboSeries))]
    uniqueSeries.unshift("ALL")
    this.series = uniqueSeries
    this.seriesImgLinks = [...new Set(this.series.map(item => "../assets/"+item+".jpg"))]
    console.log(uniqueSeries)
    // const uniqueCharacter = [...new Set(this.amiibos.map(item => item.character))]
    // console.log(uniqueCharacter)
    // const uniqueName = [...new Set(this.amiibos.map(item => item.name))]
    // console.log(uniqueName)  src/assets/Super Smash Bros..jpg /Users/user/classwork/week_07/day_05/amiibo/src/assets/Super Smash Bros..jpg
    const uniqueType = [...new Set(this.amiibos.map(item => item.type))]
    

    eventBus.$on('amiibo-selected', (amiibo) => {
      this.selectedAmiibo = amiibo
    })

    eventBus.$on('series-selected', (series) => {
      if (series==="ALL") {
        this.filteredAmiibos = this.amiibos
      }
      else {
        this.filterAmiibos(series)
      }
      
    }),

    eventBus.$on('close-Window', () => {
      this.selectedAmiibo = null
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
  color: #2c3e50;
  margin-top: 0px;
  padding:0;
  justify-content: center;
  justify-items: center;
  text-justify:auto;
}

#title {
  grid-area: title;
  padding:0;
  margin: 0;
  align-content: center;
  background-color: white;
  text-align: center;
  
}

#image_logo{
  margin-left: 1fr;
  margin-right: auto;
  height:100px;
  align-self: center;
}

#filters{
  grid-area: filters;
  display:flex;
  flex-direction: column;
}

#list-container {
  grid-area: listcontainer;
  display:flex;
  flex-direction: column;
  overflow-y: scroll;
  
  /* background-image: url(./assets/background.jpg); */
  
}

#bg {
  z-index: -2;
  filter: blur(5px) opacity(0.5);
  
  color:rgba(0, 0,0, 0.5); 
  position:fixed;
  bottom:0;
}



#list{
  grid-area: list;
  
}

#details{
  position: fixed;
  align-self: center;
  width: auto;
  top: 50%;
  bottom: 50%;
  grid-area: details;
  margin: 0;
  padding: 0;
}

#grid-container {
  display: grid;
  grid-template-columns: 1fr 4fr;
  grid-template-rows: 100px 1fr ;
  grid-template-areas: 
      "filters title"
      "filters listcontainer";
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}

template {
  margin: 0px;
  padding: 0px;
}
</style>

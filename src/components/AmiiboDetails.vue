<template>
  <section>
      <div id="details-wrapper">
        <div id="inside-wrapper">
            <div>
                <h3>{{selectedAmiibo.name}} from {{selectedAmiibo.amiiboSeries}}</h3>       
                <p>CHARACTER: {{selectedAmiibo.character}}</p>
                <p>GAME SERIES: {{selectedAmiibo.gameSeries}}</p>
                <!-- <p v-for="(release, index) in this.selectedAmiibo.release" :release="release" :key="index">  -->
                    <p id="release-dates">
                    RELEASE DATES: <br>
                    Autstralia:{{Object.values(selectedAmiibo.release)[0]}} <br>
                    Europe:    {{Object.values(selectedAmiibo.release)[1]}}  <br>
                    Japan:     {{Object.values(selectedAmiibo.release)[2]}} <br>
                    USA:       {{Object.values(selectedAmiibo.release)[3]}}
                    
                    </p>
                <p>TYPE: {{selectedAmiibo.type}}</p>
                <button @click="closeWindow">Close</button>
            </div>
            <div>
                <img :src="selectedAmiibo.image" alt="amiibo_image">
            </div>
        </div>
      </div>
  </section>
</template>

<script>
import {eventBus} from '../main.js'

export default {
    name: 'amiibo-details',
    props: ['selectedAmiibo'],
    data() {
        return {
            
        }
    },
    computed: {
        convertToArray() {
        }
    },
    methods: {
        closeWindow() {
            eventBus.$emit('close-Window', this.selectedAmiibo)
        },
        createReleases() {
            const releaseKeys = Object.keys(selectedAmiibo.release)
            const releaseValues = Object.values(selectedAmiibo.release)
            
            

        }
    }
}
</script>

<style scoped>
img {
    max-width:200px;
}

#details-wrapper {
    box-shadow:15px 15px 15px rgba(0,0,0,0.5);
    border-collapse: collapse;
    border-radius: 15px;
    width: 600px;
    
  
  
  
  text-align: center;
}

#inside-wrapper {
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: rgba(255,240,199,0.8);
    border: solid 1px black;
    border-radius: 15px;
    padding:15px;
}

#release-dates {
    text-align: left;
}


</style>
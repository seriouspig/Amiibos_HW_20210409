<template>
<div id="button" @click="chooseSeries">
  <!-- {{series}} -->
  
 <img  :src="require(`@/assets/${series}.jpg`)" alt="series_image" id="series-logo"> 
 
</div>
</template>

<script>
import {eventBus} from '../main.js'

export default {
    name: "filter-button",
    props: ['amiibos', 'series', 'serie'],
    data() {
        return {
            
        }
    },
    methods: {
        chooseSeries() {
            eventBus.$emit('series-selected', this.series)
            console.log(this.serie)
        },

    }
}
</script>

<style scoped>

#button {
    height: 100px;
    /* background-image: url(../assets/Super Smash Bros..jpg);
    background-size: 100% 100%;
    background-repeat: no-repeat;
    background-position-x: center; */
    border: solid 1px black;
}

#button:hover {
    
    border: solid 5px orange;  
}

#series-logo{
    max-width: 100%;

    
}

#series-logo:hover{
    filter: sepia(100%) hue-rotate(45deg);
    box-shadow: inset 10px 10px 10px black;
    
}

</style>
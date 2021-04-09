<template>
  <button @click="chooseSeries">{{series}}</button>
</template>

<script>
import {eventBus} from '../main.js'

export default {
    name: "filter-button",
    props: ['amiibos', 'series'],
    data() {
        return {
            
        }
    },
    methods: {
        chooseSeries() {
            eventBus.$emit('series-selected', this.series)
        }
    }
}
</script>

<style scoped>
button {
    

}
</style>
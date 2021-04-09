<template>
  <section>
      <div @click="handleClick" id="list_item">
      {{amiibo.name}} from {{amiibo.amiiboSeries}}
      <img :src="amiibo.image" alt="amiibo_image">
      </div>
  </section>
</template>

<script>
import {eventBus} from '../main.js'

export default {
    name: 'amiibo-item',
    props: ['amiibo'],
    methods: {
        handleClick() {
            eventBus.$emit('amiibo-selected', this.amiibo);
        }
    }

}
</script>

<style scoped>
img {
    height: 50px;
}

#list_item {
    border-style: solid;
    border-width: 1px;
    margin: 2px;
    width:500px;
}

</style>
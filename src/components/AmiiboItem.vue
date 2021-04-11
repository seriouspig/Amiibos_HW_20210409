<template>
  <section>
      <div  @click="handleClick" id="list_item">
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
    /* border-style: solid;
    border-width: 1px; */
    margin: auto;

    width: auto;
    padding: 0;
    justify-content: center;
    text-align: center;
}
    
#text {
    text-align:center;
    font-weight: bold;
}



#list_item:hover {
    background-color: rgba(10,10,10,0.1);
    cursor: pointer;
    /* transform: scale(1.5); */
}

</style>
<template>
  <section>
      <h3>{{selectedAmiibo.name}} from {{selectedAmiibo.amiiboSeries}}</h3>
      <img :src="selectedAmiibo.image" alt="amiibo_image">
      <p>CHARACTER: {{selectedAmiibo.character}}</p>
      <p>GAME SERIES: {{selectedAmiibo.gameSeries}}</p>
      <p v-for="(release, index) in this.selectedAmiibo.release" :key="index"> {{selectedAmiibo.release[index]}}</p>
      <p>TYPE: {{selectedAmiibo.type}}</p>
  </section>
</template>

<script>
export default {
    name: 'amiibo-details',
    props: ['selectedAmiibo'],
    data() {
        return {
            
        }
    }
}
</script>

<style scoped>
img {
    height:200px;
}
</style>
<template>
  <section>
      {{amiibo.name}} from {{amiibo.amiiboSeries}}
      <img :src="amiibo.image" alt="amiibo_image">
  </section>
</template>

<script>
export default {
    name: 'amiibo-item',
    props: ['amiibo']

}
</script>

<style scoped>
img {
    height: 50px;
}

</style>
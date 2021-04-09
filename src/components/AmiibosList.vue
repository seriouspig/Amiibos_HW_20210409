<template>
  <section>
      <ul>
          <amiibo-item v-for="(amiibo, index) in amiibos" :amiibo="amiibo" :key="index" />
      </ul>
  </section>
</template>

<script>
import AmiiboItem from './AmiiboItem.vue'

export default {
    name: 'amiibos-list',
    props: ['amiibos'],
    components: {
        'amiibo-item': AmiiboItem
    }
    

}
</script>

<style>

</style>
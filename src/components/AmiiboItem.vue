<template>
  <section>{{amiibo.name}} from {{amiibo.amiiboSeries}}</section>
</template>

<script>
export default {
    name: 'amiibo-item',
    props: ['amiibo']

}
</script>

<style>

</style>
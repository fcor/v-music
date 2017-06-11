<template lang="pug">
  li.artist
    h2.name: a(:href="artist.url" target="_blank") {{ artist.name }}
    img(:src="artist.image[2]['#text']")
</template>

<script>
export default {
  name: 'artist',
  props: ['artist']
}
</script>

<style lang="stylus" scoped>
li.artist
    display inline-block
    padding 5px
    margin 10px
    border 2px solid #41B883
    border-radius 5px
  img
    border-radius 5px
h2.name
  text-decoration none

</style>

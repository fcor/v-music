<template lang="pug">
  #app
    img(src='dist/logo.png')
    h1 V-Music
    h2 Selecciona el pais para ver los artistas mas escuchados en Last.fm
    select(v-model="selectedCountry")
      option(v-for="country in countries" :value="country.value") {{ country.name }}
    spinner(v-show="loading")
    ul
      artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="mbid")
</template>

<script>
import artist from './components/artist.vue'
import Spinner from './components/Spinner.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        { name:'Argentina', value: 'argentina' },
        { name:'Colombia', value: 'colombia' },
        { name:'España', value: 'spain' },
        { name:'Brasil', value: 'brazil' },
        { name:'Ecuador', value: 'ecuador' },
        { name:'Peru', value: 'peru' },
      ],
      selectedCountry: 'argentina',
      loading: true
    }
  },
  components: {
    artist,
    Spinner
  },
  methods: {
    refreshArtists() {
      const self = this
      this.loading = true
      this.artists = []
      getArtists(this.selectedCountry)
        .then(function (artists) {
          self.artists = artists
          self.loading = false
        })
    }
  },
  mounted() {
    this.refreshArtists()
  },
  watch: {
    selectedCountry() {
      this.refreshArtists()
    }
  }
}
</script>

<style lang="stylus">
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px

h1, h2
  font-weight normal

ul
  list-style-type none
  padding 0

li
  display inline-block
  margin 0 10px

a
  color #3d4e68
  text-decoration none</style>

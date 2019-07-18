<template lang="pug">
  #app
    img(src='./assets/logo.png')
    h1 {{ msg }}

    select(v-model="selectedCountry")
      option(v-for="country in countries" v-bind:value="country.value") {{ country.name }}
    spinner(v-show="loading")
    ul      
      artista(v-for="artista in artistas" v-bind:artista="artista" v-bind:key="artista.mbid")
</template>

<script>
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      msg: 'xarlesMusic',
      artistas: [],
      countries: [
        {name:'España', value: 'Spain'},
        {name:'Colombia', value: 'Colombia'},
        {name:'Argentina', value: 'Argentina'}
      ],
      selectedCountry:'spain',
      loading: true
    }
  },
  components: {
    Artista: Artist,
    Spinner
  },
  methods: {
    refreshArtists() {
      const self = this
      this.loading = true
      getArtists(this.selectedCountry)
      .then(function(artists){
        self.loading = false
        self.artistas = artists
      })
    }
  },
  mounted () {
    this.refreshArtists()
  },
  watch: {
    selectedCountry () {
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
  color #42b983
</style>

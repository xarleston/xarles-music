<template lang="pug">
  #app
    img(src='./assets/logo.png')
    h1 {{ msg }}
    ul      
      li(v-for="artista in artistas") {{ artista.name }}    
</template>

<script>
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      msg: 'xarlesMusic',
      /*
      artistas: [
        { name: 'Davis Bowie' },
        { name: 'Napalm Death' },
        { name: 'QOTSA' },
        { name: 'Blur' },
        { name: 'Rykers' }
      ]
      */
     artistas: []
    }
  },
  mounted: function() {
    const self = this
    getArtists()
    .then(function(artists){
      self.artistas = artists
    })
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

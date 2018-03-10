<template>
  <div class="row container">
    <div class="col-md-12">
      <section id="showcase">
        <div v-if="showDefault">
          <default-cards></default-cards>
        </div>
        <div v-else>
          <cards v-bind:movies='movies'></cards>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import { bus } from '../../main.js'
import Cards from './Cards.vue'
import DefaultCards from './DefaultCards.vue'

export default {
  data () {
    return {
      movies: [],
      showDefault: true
    }
  },
  components: {
    'cards': Cards,
    'default-cards': DefaultCards
  },
  created () {
    bus.$on('showContent', (data) => {
      this.movies = []
      data.results.forEach(result => {
        this.movies.push(result)
      })
    })
    bus.$on('component', (data) => {
      this.showDefault = data
    })
  }
}
</script>

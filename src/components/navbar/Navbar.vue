<template>
  <nav class="navbar navbar-expand-md navbar-light bg-light">
    <a class="navbar-brand px-md-3" href="#" style="width:100" v-on:click="showDefault"><img src="../../assets/pixos.png" alt="Logo"></a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbar" aria-controls="navbar" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbar">
      <ul class="navbar-nav">
        <nav-link-movies v-bind:link='movies' class="mt-md-3 px-md-2"></nav-link-movies>
        <nav-link-genres v-bind:link='genres' class="mt-md-3 px-md-2"></nav-link-genres>
        <search-form></search-form>
      </ul>
    </div>
  </nav>
</template>

<script>
import NavLink from './NavLink.vue'
import SearchForm from './Search.vue'
import { bus } from '../../main'

export default {
  data () {
    return {
      movies: {
        id: 'Movies'
      },
      genres: {
        id: 'Genres'
      }
    }
  },
  components: {
    'nav-link-genres': NavLink,
    'nav-link-movies': NavLink,
    'search-form': SearchForm
  },
  methods: {
    showDefault: function () {
      bus.$emit('component', true)
    }
  }
}
</script>

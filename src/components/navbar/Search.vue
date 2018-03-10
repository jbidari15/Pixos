<template>
  <form class="form-inline my-2 px-lg-5 ml-md-5">
    <input class="form-control mr-sm-2 ml-lg-5" type="text" placeholder="Search a movie" v-model="query">
    <button class="btn btn-outline-success my-md-2" type="submit"  v-on:click="getMovies">Search</button>
  </form>
</template>
<script>
import axios from 'axios'
import { bus } from '../../main'

export default {
  data () {
    return {
      query: ''
    }
  },
  methods: {
    getMovies: function (e) {
      e.preventDefault()
      axios.get('https://api.themoviedb.org/3/search/movie', {
        params: {
          api_key: 'd9dbf53e99fd477a1b9c4ae5257a669d',
          language: 'en-US',
          query: this.query
        }
      })
        .then(res => res.data)
        .then(data => {
          bus.$emit('showContent', data)
        })
    }
  }
}
</script>

<template>
  <div id="cards-container">
    <div class="card" style="width: 15rem;" v-for="movie in movies" :key="movie.id">
    <img class="card-img-top img-fluid" v-bind:src="imagePreUrl+movie.poster_path" alt="Card image cap">
    <div class="card-block">
      <a href="#" class="btn btn-primary btn-block" :id="movie.id" data-toggle="modal" data-target="#myModal" v-on:click="getMoreData">Read More</a>
    </div>
  </div>
  <modal v-bind:movieDetails="movieDetails"></modal>
  </div>

</template>

<script>
import Modal from './Modal.vue'
import axios from 'axios'

export default {
  props: ['movies'],
  data () {
    return {
      imagePreUrl: 'http://image.tmdb.org/t/p/w300',
      movieDetails: []
    }
  },
  components: {
    modal: Modal
  },
  methods: {
    getMoreData: function (e) {
      let movieId = e.target.getAttribute('id')
      let URL = `/movie/${movieId}`
      let Axios = axios.create({
        baseURL: 'https://api.themoviedb.org/3',
        params: {
          api_key: 'd9dbf53e99fd477a1b9c4ae5257a669d',
          language: 'en-US',
          append_to_response: 'videos'
        }
      })
      Axios.get(URL)
        .then(res => res.data)
        .then(data => {
          this.movieDetails = []
          this.movieDetails.push(data)
        })
    }
  }
}
</script>
<style scoped>
  #cards-container{
      display: flex;
      flex-direction: row;
      flex-wrap: wrap;
      justify-content: space-around;
  }
  .card{
    width: 10rem;
    margin: 10px 0px;
    border: 0 !important;
    box-shadow: 0 10px 20px rgba(0,0,0,0.19), 0 6px 6px rgba(0,0,0,0.23);
  }
  .btn{
    border-radius: 0% !important;
    box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
    transition: all 0.3s cubic-bezier(.25,.8,.25,1);
  }
  .btn:hover, .card:hover{
    box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22);
  }
  img{
    width: 240px;
    height: 260px;
    display: block;
    margin: auto;
    border-radius: 0 !important
  }
</style>

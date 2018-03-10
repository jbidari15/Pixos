<template>
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title text-center" id="exampleModalLabel">{{movieDetails[0].title}}</h5>

        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        <button type="button" class="btn btn-outline-warning  disabled my-1 mx-auto text-muted">Revenue: $ {{movieDetails[0].revenue}}</button>
        <button type="button" class="btn btn-outline-warning  disabled my-1 mx-auto text-muted">Budget: $ {{movieDetails[0].budget}}</button>
        <button type="button" class="btn btn-outline-warning disabled my-1 mx-auto text-muted">Length: {{movieDetails[0].runtime}} min</button>
        <button type="button" class="btn btn-outline-warning disabled my-1 mx-auto text-muted">Release Date: {{movieDetails[0].release_date}}</button>
        <h6 class="h6 m-1">Description:</h6>
        <p class="lead my-1">{{movieDetails[0].overview}}</p>

      </div>
      <div class="container">
        <a role="button" v-on:click="openYouTubeURL" class="btn btn-info btn-block mt-2">Watch Trailer</a>
        <button type="button" class="btn btn-danger btn-block mb-2" data-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  props: ['movieDetails'],
  data () {
    return {
      youTubeURL: ''
    }
  },
  methods: {
    openYouTubeURL: function (e) {
      this.youTubeURL = `https://www.youtube.com/watch?v=${this.movieDetails[0].videos.results[0].key}`
      window.open(this.youTubeURL, '_blank')
    }
  },
  beforeMount () {
    this.youTubeURL = `https://www.youtube.com/watch?v=${this.movieDetails[0].videos.results[0].key}`
  }
}

</script>
<style scoped>
a{
  color:aliceblue !important;
}
.btn{
    border-radius: 0% !important;
    box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24) ;
    transition: all 0.3s cubic-bezier(.25,.8,.25,1);
  }
  .btn:hover, .card:hover{
    box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22);
  }
</style>

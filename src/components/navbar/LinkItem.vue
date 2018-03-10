<template>
  <div class="dropdown-menu">
    <a class="dropdown-item" v-for = 'linkItem in linkItems' v-bind:key='linkItem.id' v-bind:url="linkItem.url">
      <span v-on:click="getMovies">{{ linkItem.name }}</span>
    </a>
  </div>
</template>

<script>
import getData from '../../services/getData'
import { bus } from '../../main'

export default {
  props: ['linkItems'],
  data () {
    return {
    }
  },
  methods: {
    getMovies: function (e) {
      let url = e.target.parentNode.getAttribute('url')
      getData(url) // url is coming from parent component as props
        .then(data => {
          bus.$emit('showContent', data)
          bus.$emit('component', false)
        })
    }
  }
}
</script>

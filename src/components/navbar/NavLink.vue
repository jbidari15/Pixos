<template>
  <li class="nav-item dropdown">
    <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMenuLink" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
      {{ this.link.id }}
    </a>
    <link-item v-bind:linkItems= 'linkItems'></link-item>
  </li>
</template>

<script>
import Axios from '../../services/Api'
import LinkItem from './LinkItem.vue'
export default {
  props: ['link'],
  data () {
    return {
      linkItems: [],
      linkObj: this.linkItems
    }
  },
  components: {
    'link-item': LinkItem
  },
  created () {
    if (this.link.id == 'Movies') {
      this.linkItems = [
        {
          id: 1,
          name: 'Popular',
          url: '/movie/popular?'
        },
        {
          id: 2,
          name: 'Top Rated',
          url: '/movie/top_rated?'
        },
        {
          id: 3,
          name: 'Now Playing',
          url: '/movie/now_playing?'
        },
        {
          id: 4,
          name: 'Upcoming',
          url: '/movie/upcoming?'
        }
      ]
    } else {
      Axios.get('/genre/movie/list?')
        .then(res => {
          let dataArr = res.data.genres
          this.linkItems = dataArr
          this.linkItems.forEach(item => {
            item.url = `/genre/${item.id}/movies?`
          })
        })
    }
  }
}
</script>

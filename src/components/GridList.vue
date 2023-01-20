<template>
  <div>
    <div class="filters">
      <label for="sort">Sort by</label>
      <select
        name="sort"
        v-model="photo.orderBy"
        @change="fetchPhotos(photo.page, $event.target.value)"
      >
        <option value="latest">Latest</option>
        <option value="oldest">Oldest</option>
        <option value="popular">Popular</option>
      </select>
    </div>

    <div class="loader" v-if="photo.loadState == LOAD_STATE.LOADING"></div>

    <div class="grid" v-if="photo.loadState == LOAD_STATE.SUCCESS">
      <GridItem v-for="photo in photo.photos" :key="photo.id" :photo="photo"/>
    </div>
    <Pagination @onPageChanged="fetchPhotos"/>
  </div>
</template>

<script>
import GridItem from './GridItem'
import Pagination from './Pagination'
import partials from '@/store/partials'

import { mapState, mapActions } from 'vuex'

export default {
  data() {
    return {
      ...partials
    }
  },
  components: {
    GridItem,
    Pagination
  },
  methods: {
    fetchPhotos(page, order) {
      this.$store.dispatch('photo/fetch', {
        page,
        order: this.photo.orderBy
      })
    }
  },
  computed: mapState(['photo']),
  mounted() {
    this.fetchPhotos(this.photo.page)
  }
}
</script>


<template>
  <div class="grid__item card">
    <div class="card__body">
      <a :href="photo.links.download" target="_blank">
        <img :src="photo.urls.regular" :alt="photo.description">
      </a>
    </div>
    <div class="card__footer media">
      <img :src="photo.user.profile_image.medium" :alt="photo.user.name" class="media__obj">
      <div class="media__body">
        <a :href="photo.user.links.html" target="_blank">{{ photo.user.name }}</a>

        <div>
          <span class="card__likes">
            <i class="fa fa-heart"></i>
            {{ photo.likes }}
          </span>
          
          <span class="card__date">
            <i class="fa fa-calendar-o"></i>
            {{ photo.created_at | formatDate }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment'

export default {
  props: {
    photo: {
      type: Object,
      required: true
    }
  },
  filters: {
    formatDate(value) {
      return moment(value).format('LL')
    }
  }
}
</script>

<template lang="pug">
  .container
    transition-group(name="fade" tag="div")
      .columns(v-if="track && track.album"
               v-bind:key="track.id")
        .column.is-3.has-text-centered
          figure.media-left
            p.image
              img(:src="track.album.images[0].url")

        .column.is-8
          .panel
            .panel-heading
              h1.title {{ track.name }}
            .panel-block
              .article.media
                .media.content
                  .content
                    ul(v-for="(v, k) in track")
                      li
                        strong {{ k }}:&nbsp;
                        span {{ v }}
</template>

<script>
import trackService from '~/plugins/track'

export default {
  data () {
    return {
      track: {}
    }
  },

  head () {
    return {
      title: this.track.name
    }
  },

  asyncData ({ params }) {
    const id = params.id

    return trackService.getById(id)
        .then(res => { return { track: res } })
  } 
}
</script>

<style lang="scss" scoped>
  .columns {
    margin: 20px;
  }

  .button-bar {
    margin-top: 20px;
  }
</style>

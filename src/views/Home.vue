<template>
  <div id="home" class="pa-4">
    <v-container fluid>
      <h3 class="headline font-weight-medium">Recommended</h3>
      <v-row>
        <v-col
          cols="12"
          sm="6"
          md="4"
          lg="3"
          v-for="i in loading ? 10 : 12"
          :key="i"
          class="mx-xs-auto"
        >
          <v-skeleton-loader type="card-avatar" :loading="loading">
            <video-card
              :card="{ maxWidth: 350 }"
              :video="video"
              :channel="channel"
            ></video-card>
            <!-- <v-card
              class="content-bg card mx-auto"
              max-width="350"
              flat
              tile
              router
              to="/watch/12"
            >
              <v-img
                src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
                height="200px"
              ></v-img>
              <v-row no-gutters>
                <v-col cols="2">
                  <v-list-item class="pl-0 pt-3" router to="/channels/12">
                    <v-list-item-avatar color="grey darken-3">
                      <v-img
                        class="elevation-6"
                        src="https://randomuser.me/api/portraits/men/1.jpg"
                      ></v-img>
                    </v-list-item-avatar>
                  </v-list-item>
                </v-col>
                <v-col>
                  <v-card-title class="pl-2 pt-3 subtitle-1 font-weight-bold">
                    Top western road trips
                  </v-card-title>

                  <v-card-subtitle class="pl-2 pb-0">
                    1,000 miles of wonder
                  </v-card-subtitle>
                  <v-card-subtitle class="pl-2 pt-0">
                    9.6k views<v-icon>mdi-circle-small</v-icon>6 hours ago
                  </v-card-subtitle>
                </v-col>
              </v-row>
            </v-card> -->
          </v-skeleton-loader>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import videoCard from '@/components/VideoCard'

export default {
  name: 'Home',
  data: () => ({
    loading: true,
    video: {
      url: '/watch/12',
      thumb: 'https://cdn.vuetifyjs.com/images/cards/sunshine.jpg',
      title: 'Top western road trips',
      views: '9.6k',
      createdAt: '6 hours ago'
    },
    channel: {
      url: '/channels/12',
      avatar: 'https://randomuser.me/api/portraits/men/1.jpg'
    }
  }),
  components: {
    videoCard
  },
  mounted() {
    setTimeout(() => {
      this.loading = false
    }, 3000)
  }
}
</script>

<style lang="scss">
.card {
  background: #f9f9f9 !important;
}
</style>

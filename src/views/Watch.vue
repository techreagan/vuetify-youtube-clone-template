<template>
  <div id="watch">
    <v-container fluid>
      <v-row>
        <v-col cols="11" class="mx-auto">
          <v-row>
            <v-col cols="12" sm="12" md="8" lg="8">
              <v-responsive>
                <video controls>
                  <source src="../assets/video.mp4" type="video/mp4" />
                </video>
              </v-responsive>
              <v-card flat tile class="card">
                <v-card-title class="pl-0 pb-0"
                  >Attendance Management System</v-card-title
                >
                <div class="d-flex justify-space-between" id="btns">
                  <v-card-subtitle
                    class="pl-0 pt-0 pb-0 subtitle-1"
                    style="line-height: 2.4em"
                  >
                    9.6k views<v-icon>mdi-circle-small</v-icon>6 hours ago
                  </v-card-subtitle>
                  <v-card-actions class="pt-0 grey--text">
                    <v-btn text><v-icon>mdi-thumb-up</v-icon> 1.5k</v-btn>
                    <v-btn text><v-icon>mdi-thumb-down</v-icon> 1.5k</v-btn>
                    <v-btn text><v-icon>mdi-share</v-icon> Share</v-btn>
                    <v-btn text><v-icon>mdi-playlist-plus</v-icon> Save</v-btn>
                  </v-card-actions>
                </div>
              </v-card>
            </v-col>
            <v-col cols="12" sm="12" md="4" lg="4">
              <hr class="grey--text" />
              <h4 class="mb-3 mt-3">Up next</h4>
              <div v-for="i in 10" :key="i" class="mb-5">
                <v-skeleton-loader
                  class="mx-auto"
                  type="list-item-avatar-three-line"
                  :loading="loading"
                  tile
                  large
                >
                  <v-card class="card" tile flat>
                    <v-row no-gutters>
                      <v-col class="mx-auto" cols="12" sm="8" md="5" lg="5">
                        <!-- <v-responsive max-height="100%"> -->
                        <v-img
                          class="align-center"
                          src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
                        >
                        </v-img>
                        <!-- </v-responsive> -->
                      </v-col>
                      <v-col>
                        <div class="ml-2">
                          <v-card-title
                            class="pl-2 pt-0 subtitle-1 font-weight-bold"
                            style="line-height: 1"
                          >
                            Top western road trips
                          </v-card-title>

                          <v-card-subtitle
                            class="pl-2 pt-2 pb-0"
                            style="line-height: 1"
                          >
                            Tech Reagan<br />
                            9.6k views<v-icon>mdi-circle-small</v-icon>6 hours
                            ago
                          </v-card-subtitle>
                          <!-- <v-card-subtitle>

                        </v-card-subtitle> -->
                        </div>
                      </v-col>
                    </v-row>
                  </v-card>
                </v-skeleton-loader>
              </div>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  data: () => ({
    loading: true
  }),
  mounted() {
    setTimeout(() => {
      this.loading = false
    }, 100)
  }
}
</script>

<style lang="scss">
video {
  max-width: 100%;
  /* min-height: 360px; */
  /* width: 640px;
  height: 360px; */
}

#btns {
  border-bottom: 1px solid #e0d8d8;
  button {
    color: #7f7f7f;
  }
}
</style>

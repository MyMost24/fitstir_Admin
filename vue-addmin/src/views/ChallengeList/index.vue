<template>
  <v-content>
    <v-container class="align-center" v-if="response">
      <h2 >Challenge

      </h2>

      <v-btn color="info" @click="$router.push('/app/createchallenge/index')"
             style="margin-top: 10px;"
      >
        <v-icon color="white">mdi-plus</v-icon>
        Create Challenge
      </v-btn>

      <div
          class="flex flex-wrap sm:-m-4 -mx-4 -mb-10  justify-center md:justify-start items-center md:items-start mt-8">
        <div style="width:300px;" >
          <v-layout class="row">
            <v-flex md6 xs12 v-for="list,index in CHALLENGELISTS" :key="index">
              <v-card class="p-4  w-full  justify-center items-center"
                      @click="$router.push(`/app/challenge/index?id=${list.id}`)">

                <img style="height:200px; width:200px;" v-if="list.image" :src="list.image" alt="">
                <div class="">{{ list.name }}</div>
                <v-btn
                    color="red"
                    @click="getdataDialogid(list.id)"
                >
                  <v-icon color="white">mdi-cog-outline</v-icon>
                </v-btn>

              </v-card>
            </v-flex>
          </v-layout>
        </div>
      </div>

      <v-dialog
          v-model="dialog"
          max-width="350"
      >
        <v-card>
          <v-card-title class="headline"> Setting Playlsit Video</v-card-title>
          <v-form>
            <v-container>
              <v-layout justify-center items-center>
                <v-flex row>
                  <v-btn
                      class="pa-md-5 mx-lg-auto"
                      width="300"
                      color="green"
                      @click="$router.push(`/Addvideoplaylist?id=${dataDialog}`)"
                  >
                    <v-icon
                    >
                      mdi-folder-multiple-plus
                    </v-icon>
                    ADD Video
                  </v-btn>
                  <v-btn
                      class="pa-md-5 mx-lg-auto mt-2"
                      width="300"
                      color="primary"
                      @click="$router.push(`/playlistpage?id=${dataDialog}`)"
                  >
                    <v-icon>mdi-eye</v-icon>
                    My playlist
                  </v-btn>
                  <v-btn
                      class="pa-md-5 mx-lg-auto mt-2"
                      width="300"
                      color="red"
                      @click="deletePlaylist()"
                  >
                    Remove Playlist
                  </v-btn>
                </v-flex>
              </v-layout>
            </v-container>
          </v-form>
        </v-card>
      </v-dialog>



    </v-container>
  </v-content>
</template>

<script>
import {call, sync} from 'vuex-pathify'

export default {
  name: "index",
  data: () => ({
    response: false,
    dataDialog:null,
    dialog : false,


  }),
  computed: {
    CHALLENGELISTS: sync('challenge/challengeLists')

  },
  async mounted() {
    await this.loadData()
  },
  methods: {
    ...call('challenge/*'),
    async loadData() {
      this.challenge = await this.$store.dispatch('challenge/getListChallenge')
      this.CHALLENGELISTS = this.challenge
      console.log(this.CHALLENGELISTS)
      this.response = true
    },
    async getdataDialogid(id) {
      this.dialog = true
      this.dataDialog = id
    },


  }
}
</script>

<style scoped>

</style>
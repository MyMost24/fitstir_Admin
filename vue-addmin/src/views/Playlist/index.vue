<template>
    <v-container>
      <div v-if="response">
        <p class="text-4xl">Play List</p>
        <v-text-field outlined v-model="search" append-icon="mdi-magnify" label="Search" single-line
                      hide-details></v-text-field>
        <br>
        <v-btn color="info" @click="$router.push('/app/createplaylist/index')"
        >
          <v-icon color="white">mdi-playlist-plus</v-icon>
          Create playlist
        </v-btn>
        <v-data-table :headers="headers" :items="PLAYLISTS" :search="search" class="elevation-1">
          <template v-slot:body="{ items }">
            <tbody>
            <tr v-for="playlist,index in items" :key="index">

              <td class="t-w-64  t-p-4">
                <div class="t-w-full t-flex t-flex-row t-items-center w3-medium ">
                  <img width="150" height="150" :src="$url+ playlist.image" alt="">


                </div>
              </td>
              <td>
                {{ playlist.name }}
              </td>

              <td>
                <v-btn color="purple" text @click="$router.push(`/app/playlistpage/index?id=${playlist.id}`)">
                  <v-icon>mdi-play-circle-outline</v-icon>
                  Play
                </v-btn>
              </td>

              <td>
                <v-btn @click="$router.push(`/app/playlistdetail/index?playlist=${playlist.id}`)" text color="info">
                  <v-icon>mdi-eye</v-icon>
                  ดูข้อมูล
                </v-btn>


                <v-btn @click="deletePlaylist(playlist.id)" color="red" text>
                  <v-icon>mdi-delete</v-icon>
                  Delete
                </v-btn>
              </td>
            </tr>
            </tbody>
          </template>
        </v-data-table>
      </div>
    </v-container>
</template>


<script>
import {call, sync} from 'vuex-pathify'

export default {
  name: "playlist",
  data: () => ({
    response: false,
    search: '',
    headers: [
      {
        text: 'play list name',
        align: 'start',
        value: 'title'
      },
      {
        text: 'play',
        value: 'playlist'

      },
      {
        text: 'Name',
        value: 'name',
      },
      {
        text: 'setting',
        filterable: false,
      }
    ]


  }),
  computed: {
    PLAYLISTS: sync('playlist/playLists')
  },
  async mounted() {
    await this.loadData()
  },
  methods: {
    ...call('playlist/*'),
    async loadData() {
      this.PLAYLISTS = await this.$store.dispatch('playlist/getPlaylist')
      console.log(this.PLAYLISTS)
      this.response = true
      return this.PLAYLISTS
    },
    async deletePlaylist(pk){
      if (confirm('Do you want to delete?')) {

        await this.$store.dispatch('playlist/deletePlaylist', pk)
        await this.loadData()
      }
    }
  }
}
</script>

<style scoped>

</style>
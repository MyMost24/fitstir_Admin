<template>
    <v-container>
      <v-tabs color="primary" class="mt-4" slider-color="primary">
        <v-tab>
          ข้อมูลทั่วไป
        </v-tab>
        <v-tab-item>

          <div class="container flex flex-col justify-center items-center mx-auto " >
            <div class="w-full lg:w-8/12 px-7  items-center ">
              <div class="relative flex flex-col min-w-0 break-words  mb-6 shadow-lg rounded-lg bg-gray-200 border-0">
                <div class="rounded-t bg-white mb-0 px-6 py-6">
                  <div class="text-center flex justify-between">
                    <h6 class="text-gray-800 text-4xl  ">Playlist Edit</h6>
                    <v-btn
                            @click="updatePlaylist()"
                            class="ma-2"
                            outlined
                            color="indigo"
                    >
                      Save
                    </v-btn>
                  </div>
                </div>
                <div class="flex-auto px-4 lg:px-10 py-10 pt-0">
                  <h6 class="text-gray-500 text-sm mt-3 mb-6 font-bold uppercase">
                    Playlist Detail
                  </h6>
                  <img crossorigin="anonymous" style="height: 300px;" id="imageid"
                       v-if="PLAYLISTCHOOSE.image" class=" t-h-32 t-w-64"
                       :src="$url+ PLAYLISTCHOOSE.image"
                       ref="image" alt=""><br>

                  <input accept="image/jpeg,image/jpg,image/*" type="file" id="fileUpload" ref="file"
                         v-on:change="handleFileUpload()"/>
                  <br><br>

                  <form>
                    <div class="flex flex-wrap">
                      <div class="w-full lg:w-6/12 px-4">
                        <div class="relative w-full mb-3">
                          <label
                                  class="block uppercase text-gray-700 text-xs font-bold mb-2"
                                  htmlFor="grid-password"
                          >
                            Name
                          </label>
                          <input
                                  v-model="PLAYLISTCHOOSE.name"
                                  type="text"
                                  class="px-3 py-3 placeholder-gray-400 text-gray-700 bg-white rounded text-sm shadow focus:outline-none focus:shadow-outline w-full ease-linear transition-all duration-150"
                                  value="lucky.jesse"
                          />
                        </div>
                      </div>
                    </div>
                    <div class="flex flex-wrap">
                      <div class="w-full lg:w-6/12 px-4">
                        <div class="relative w-full mb-3">
                          <label
                                  class="block uppercase text-gray-700 text-xs font-bold mb-2"
                                  htmlFor="grid-password"
                          >
                            Detail
                          </label>
                          <textarea
                                  v-model="PLAYLISTCHOOSE.description"
                                  type="text"
                                  class="px-3 py-3 placeholder-gray-400 text-gray-700 bg-white rounded text-sm shadow focus:outline-none focus:shadow-outline w-full ease-linear transition-all duration-150"
                                  rows="4"
                          >

                  </textarea
                  >
                        </div>
                      </div>
                    </div>
                  </form>
                </div>
              </div>
            </div>
          </div>

        </v-tab-item>
        <v-tab>
          รายการวีดีโอ
        </v-tab>
        <v-tab-item>
          <p class=" text-4xl">
            Add video Playlist
          </p>
          <br>
          <v-dialog
              v-model="dialog1"
              fullscreen
              hide-overlay
          >
            <template v-slot:activator="{ on, attrs }">
              <v-btn
                  class="t-text-blue-600"
                  color="primary"
                  dark
                  v-bind="attrs"
                  v-on="on"
              >
                <v-icon color="white">mdi-movie-open</v-icon>
                Add Video
              </v-btn>
            </template>
            <v-card>
              <v-toolbar
                  dark
                  color="primary"
              >
                <v-btn
                    icon
                    dark
                    @click="dialog1 = false"
                > X <!--                        <v-icon>mdi-close</v-icon>-->
                </v-btn>
                <v-toolbar-title>Choose Video</v-toolbar-title>
                <v-spacer></v-spacer>
              </v-toolbar>
              <v-data-table
                  :headers="headers"
                  :items="videos"
              >
                <template v-slot:body="{ items }">
                  <tbody>
                  <tr v-for="list,index in items"
                      :key="index"
                  >
                    <td>
                      <img :src="list.image" alt="" width="100" height="100">
                    </td>
                    <td class="w3-large">{{ list.name }}</td>
                    <td>
                      <v-btn text color="primary" @click="chooseVideo(list.id)" border>
                        <v-icon>mdi-check</v-icon>
                        Select
                      </v-btn>
                    </td>
                  </tr>
                  </tbody>
                </template>
              </v-data-table>
            </v-card>
          </v-dialog>
          <br>

          <v-data-table
              :headers="headers1"
              :items="videoplaylist"
          >
            <template v-slot:body="{ items }">
              <tbody>
              <tr v-for="list,index in items" :key="index">
                <td>
                  <img :src="$url+list.video.image" alt="" width="100" height="100">
                </td>
                <td class="w3-large">{{ list.video.name }}</td>
                <td>

                  <v-btn color="purple" text @click="openVideoPlayer(list)">
                    <v-icon>mdi-play-circle-outline</v-icon>
                    Preview
                  </v-btn>

                </td>
                <td>
                  <v-btn text color="red" @click="remove(list.id)" border>
                    <v-icon>mdi-cup-off-outline</v-icon>
                    remove
                  </v-btn>
                </td>
              </tr>
              </tbody>
            </template>
          </v-data-table>
          <div
                  class="relative flex flex-col min-w-0 break-words w-full mb-6 shadow-lg rounded"
          >
            <div class="rounded-t mb-0 px-4 py-3 border-0">
              <div class="flex flex-wrap items-center">
                <div class="relative w-full px-4 max-w-full flex-grow flex-1">
                  <h3 class="font-semibold text-lg"
                  >
                    Add video Playlist
                  </h3>
                </div>
              </div>
            </div>
            <div class="block w-full overflow-x-auto">
              <table
                      class="items-center w-full bg-transparent border-collapse"
                      :headers="headers1"
                      :items="videoplaylist"
              >
                <thead >
                <tr>
                  <th
                          class="px-6 align-middle border border-solid py-3 text-xs uppercase border-l-0
                          border-r-0 whitespace-no-wrap font-semibold text-left"
                          >
                    Image
                  </th>
                  <th
                          class="px-6 align-middle border border-solid py-3 text-xs uppercase border-l-0
                          border-r-0 whitespace-no-wrap font-semibold text-left"
                  >
                    Name
                  </th>
                  <th
                          class="px-6 align-middle border border-solid py-3 text-xs uppercase border-l-0
                          border-r-0 whitespace-no-wrap font-semibold text-left"
                  >
                    Play
                  </th>
                  <th
                          class="px-6 align-middle border border-solid py-3 text-xs uppercase border-l-0
                          border-r-0 whitespace-no-wrap font-semibold text-left"
                  >
                    Manage
                  </th>
                </tr>
                </thead>
                <tbody>
                <tr
                >
                  <th>

                  </th>
                  <th>

                  </th>
                  <th>

                  </th>
                  <th>

                  </th>
                </tr>
                </tbody>
              </table>
            </div>
          </div>
        </v-tab-item>
      </v-tabs>

      <v-dialog
          v-model="dialog"
          v-if="videoData"
          width="650px"
      >
        <v-card>
          <v-card-title>

            <h2 v-if="videoData.video">{{ videoData.video.name }}</h2>
            <v-spacer></v-spacer>
            <v-btn @click="dialog = false">X</v-btn>
          </v-card-title>
          <video style="width:100%;" controls autoplay v-if="videoData.video"
                 :src="$url+videoData.video.video"></video>
        </v-card>
      </v-dialog>


    </v-container>
</template>

<script>
import {call, sync} from 'vuex-pathify'
import swal from "sweetalert2";
import Template from "../CreateChallenge/Template";

export default {
  name: "index",
  components: {Template},
  data: () => ({
    response: false,
    videoplaylist: [],
    videoData: {},
    videos: [],
    dialog: false,
    dialog1: false,
    headers1: [
      {
        align: 'start',
        sortable: false,
        value: 'name',
      },
      {
        text: 'Name',
        value: 'name'
      },

      {
        text: 'Play',
        value: 'play'
      },

      {
        text: 'Manage',
        value: 'manage'
      },
    ],
    headers: [
      {
        align: 'start',
        sortable: false,
        value: 'name',
      },
      {
        text: 'Name',
        value: 'name'
      },

      {
        text: 'Play',
        value: 'play'
      },

      {
        text: 'Manage',
        value: 'manage'
      },
    ],

  }),
  computed: {
    PLAYLISTCHOOSE: sync('playlist/playListChoose')
  },
  async mounted() {
    await this.loadData()
  },
  methods: {
    ...call('playlist/*'),
    loadData: async function () {
      let id = this.$route.query.playlist;
      this.playlist = await this.$store.dispatch('playlist/getPlaylistById', id)
      this.videoplaylist = await this.$store.dispatch('playlist/getVideoPlaylist', id)
      this.videos = await this.$store.dispatch('video/getListVideo')
      this.PLAYLISTCHOOSE = this.playlist
      this.response = true
    },
    async handleFileUpload(e) {

      let file = this.$refs.file.files[0];
      var reader = new FileReader();
      reader.onload = async (e) => {
        this.PLAYLISTCHOOSE.image = e.target.result
        this.$refs.image.src = e.target.result
      };
      reader.onerror = function (error) {
        alert(error);
      };
      this.selectedImage = URL.createObjectURL(file)
      this.PLAYLISTCHOOSE.image = file
      // await reader.readAsDataURL(file)
      // return this.selectedImage = file
    },
    updatePlaylist: async function () {
      console.log(document.getElementById("imageid"));
      console.log(this.PLAYLISTCHOOSE.image)
      await this.$store.dispatch('playlist/updatePlaylist', this.PLAYLISTCHOOSE)
      if (!false) {
        await swal.fire(
                'สำเร็จ',
                'เพิ่มวิดีโอสำเร็จเเล้ว',
                'success'
        )
        await this.$router.push('/app/playlists/playlist')
      }


    },

    async openVideoPlayer(video) {
      this.videoData = video
      this.dialog = true
      console.log(this.videoData.video)

    },
    chooseVideo: async function (videoId, day) {
      this.videos.id = videoId
      let playlistCurrent = this.$route.query;
      console.log(Number(playlistCurrent.playlist))
      let addVideo = await this.$store.dispatch('playlist/postVideoPlaylist', {
        "video": videoId,
        "playlist": Number(playlistCurrent.playlist),
      })
      if (addVideo != false) {
        // this.dialog =false;
        swal.fire(
            'สำเร็จ',
            'เพิ่มวิดีโอสำเร็จเเล้ว',
            'success'
        )
        // this.dialog =true;
      } else {
        swal.fire(
            'ไม่สำเร็จ',
            'เพิ่มวิดีโอสำไม่เร็จเเล้ว',
            'error'
        )
      }
      await this.loadData();

    },
    remove: async function (id) {
      await this.$store.dispatch('playlist/deleteVideoPlaylist', id)
      await this.loadData();
    },

  }
}
</script>

<style scoped>

</style>
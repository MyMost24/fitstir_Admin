<template>
      <!--      <h1>Create Playlist</h1>-->
      <!--      <v-card class="t-p-8" v-if="" flat>-->
      <!--        <img id="imageid" class=" t-h-32 t-w-64" :src="selectedImage" ref="image" style="width: 300px;" alt=""><br>-->

      <!--        <input accept="image/jpeg,image/jpg,image/*" type="file" id="fileUpload" ref="file"-->
      <!--               v-on:change="handleFileUpload()"/>-->
      <!--        <br><br>-->

      <!--        <v-text-field-->
      <!--                      outlined-->
      <!--                      label="ชื่อ playlist"-->
      <!--                      type="text"-->
      <!--                      v-model="form.name"-->
      <!--        />-->
      <!--        <v-textarea-->
      <!--                    outlined-->
      <!--                    label="รายระเอียด"-->
      <!--                    type="text"-->
      <!--                    v-model="form.description"-->
      <!--        />-->

      <!--        <v-card-actions>-->
      <!--          <div class="t-w-full">-->
      <!--            <v-btn class="t-float-right" large dark @click="createPlaylist()" color="primary">-->
      <!--              <v-icon>mdi-playlist-plus</v-icon> Create Playlist-->
      <!--            </v-btn>-->
      <!--          </div>-->
      <!--        </v-card-actions>-->
      <!--      </v-card>-->
      <div class="container flex flex-col justify-center items-center mx-auto " >
        <div
              style="background-image: url()"
              class=" bg-blue-300 h-64 w-24 min-w-full
                rounded-lg shadow-md bg-cover bg-center"
      >
      </div>
          <div class="w-full  -mt-24  lg:w-8/12 px-7  justify-center ">
            <div class="relative flex flex-col min-w-0 break-words  mb-6 shadow-lg rounded-lg bg-gray-200 border-0">
              <div class="rounded-t bg-white mb-0 px-6 py-6">
                <div class="text-center flex justify-between">
                  <h6 class="text-gray-800 text-3xl">Create Playlist</h6>
                  <v-btn
                          @click="createPlaylist()"
                          class="ma-2"
                          outlined
                          color="indigo"
                  >
                    Create
                  </v-btn>
                </div>
              </div>
              <div class="flex-auto px-4 lg:px-10 py-10 pt-0">
                <h6 class="text-gray-500 text-sm mt-3 mb-6 font-bold uppercase">
                  Playlist Information
                </h6>
                <img id="imageid" class=" t-h-32 t-w-64" :src="selectedImage" ref="image" style="width: 300px;" alt=""><br>

                <input accept="image/jpeg,image/jpg,image/*" type="file" id="fileUpload" ref="file"
                       v-on:change="handleFileUpload()"/>
                <br>
                <br>
                <hr class="mt-6 border-b-1 border-gray-400" />
                <br>
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
                                v-model=" form.name"
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
                                v-model="form.description"
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
</template>

<script>
import {call, sync} from 'vuex-pathify'
import swal from "sweetalert2";

export default {
  name: "index",
  data: () => ({
    selectedImage:null,
    form: {
      name: null,
      description: null,
      image: null,
      user: null,
    }

  }),
  computed: {
    ...sync('user/*')
  },
  mounted() {

  },
  methods: {
    ...call('playlist/*'),

    async handleFileUpload() {

      let file = this.$refs.file.files[0];
      var reader = new FileReader();
      reader.onload = async (e) => {
        this.form.image = e.target.result
        this.$refs.image.src = e.target.result
      };
      reader.onerror = function (error) {
        alert(error);
      };
      console.log(file)
      this.selectedImage = URL.createObjectURL(file)
      this.form.image = file

    },
    async createPlaylist() {
      this.form.user = this.userProfile.pk
      let data = await this.$store.dispatch('playlist/createPlaylist', this.form)
      if(!false){
        await  swal.fire(
                'สำเร็จ',
                'เพิ่มวิดีโอสำเร็จเเล้ว',
                'success'
        )
        await this.$router.push('/app/playlists/playlist')
      }

      console.log(this.form)

      return data

    },
    clearForm: async function () {
      this.form = {}
    },

  },



}
</script>

<style scoped>

</style>
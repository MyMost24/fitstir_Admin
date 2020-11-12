<template>
    <v-container>
<!--      <v-card>-->
<!--        <v-card-title primary-title>-->
<!--          <h2 class="t-text-2xl  t-text-bold">-->
<!--            <v-icon class="t-text-orange-500">mdi-account</v-icon>-->
<!--            ข้อมูลผู้ใช้-->
<!--          </h2>-->
<!--        </v-card-title>-->
<!--        <v-card class="t-p-8">-->


<!--          <v-text-field v-model=" USERCHOOSE.first_name" required outlined label="First Name"-->
<!--                        prepend-inner-icon="mdi-account-card-details" type="text"/>-->
<!--          <br>-->

<!--          <v-text-field v-model=" USERCHOOSE.last_name" class="t-ml-0 md:t-ml-2" required outlined label="Last Name"-->
<!--                        prepend-inner-icon="mdi-account-card-details" type="text"/>-->
<!--          <br>-->

<!--          <v-text-field v-model=" USERCHOOSE.email" required outlined label="Email" prepend-inner-icon="mdi-email"-->
<!--                        type="email"/>-->

<!--          <v-checkbox label="ตั้งค่าเป็นแอดมิน" v-model="USERCHOOSE.is_staff"></v-checkbox>-->

<!--          <v-card-actions>-->
<!--            <div class="t-w-full">-->
<!--              <v-btn class="t-float-right" large dark @click="updateUser()" color="primary">-->
<!--                <v-icon>mdi-account-add-outline</v-icon>-->
<!--                แก้ไขผู้ใช้-->
<!--              </v-btn>-->
<!--            </div>-->
<!--          </v-card-actions>-->
<!--        </v-card>-->
<!--      </v-card>-->
      <div class="container flex flex-col justify-center items-center mx-auto " >
        <div
                style="background-image: url()"
                class=" bg-blue-300 h-64 w-24 min-w-full
                rounded-lg shadow-md bg-cover bg-center"
        >
        </div>
        <div class="w-full lg:w-8/12 px-7  -mt-24  justify-center ">
          <div class="relative flex flex-col min-w-0 break-words  mb-6 shadow-lg rounded-lg bg-gray-200 border-0">
            <div class="rounded-t bg-white mb-0 px-6 py-6">
              <div class="text-center flex justify-between">
                <h6 class="text-gray-800 text-xl font-bold">Edit User</h6>
                <v-btn
                        @click="updateUser()"
                        class="ma-2"
                        outlined
                        color="indigo"
                >
                  Save
                </v-btn>

              </div>
            </div>
            <div class="flex-auto px-4 lg:px-10 py-10 pt-0">
              <form>
                <h6 class="text-gray-500 text-sm mt-3 mb-6 font-bold uppercase">
                  User Information
                </h6>
                <div class="flex flex-wrap">
                  <div class="w-full lg:w-6/12 px-4">
                    <div class="relative w-full mb-3">
                      <label
                              class="block uppercase text-gray-700 text-xs font-bold mb-2"
                              htmlFor="grid-password"
                      >
                        Firstname
                      </label>
                      <input
                              v-model=" USERCHOOSE.first_name"
                              type="text"
                              class="px-3 py-3 placeholder-gray-400 text-gray-700 bg-white rounded text-sm shadow focus:outline-none focus:shadow-outline w-full ease-linear transition-all duration-150"
                              value="lucky.jesse"
                      />
                    </div>
                  </div>
                  <div class="w-full lg:w-6/12 px-4">
                    <div class="relative w-full mb-3">
                      <label
                              class="block uppercase text-gray-700 text-xs font-bold mb-2"
                              htmlFor="grid-password"
                      >
                        Lastname
                      </label>
                      <input
                              v-model=" USERCHOOSE.last_name"
                              type="text"
                              class="px-3 py-3 placeholder-gray-400 text-gray-700 bg-white rounded text-sm shadow focus:outline-none focus:shadow-outline w-full ease-linear transition-all duration-150"
                              value="lucky.jesse"
                      />
                    </div>
                  </div>
                  <div class="w-full lg:w-6/12 px-4">
                    <div class="relative w-full mb-3">
                      <label
                              class="block uppercase text-gray-700 text-xs font-bold mb-2"
                              htmlFor="grid-password"
                      >
                        E-mail
                      </label>
                      <input
                              v-model=" USERCHOOSE.email"
                              type="text"
                              class="px-3 py-3 placeholder-gray-400 text-gray-700 bg-white rounded text-sm shadow focus:outline-none focus:shadow-outline w-full ease-linear transition-all duration-150"
                              value="Lucky"
                      />
                    </div>
                  </div>
                </div>
                <v-checkbox label="ตั้งค่าเป็นแอดมิน" v-model="USERCHOOSE.is_staff"></v-checkbox>
              </form>
            </div>
          </div>
        </div>
      </div>
    </v-container>

</template>

<script>
import {call, sync} from 'vuex-pathify'
import swal from 'sweetalert2'

export default {
  name: "index",
  data: () => ({
    user: []
  }),
  computed: {
    USERCHOOSE: sync('user/userChoose')

  },
  async mounted() {
    await this.load()
  },
  methods: {
    ...call('user/*'),
    load: async function () {
      let idUser = this.$route.query.user;
      this.user = await this.$store.dispatch('user/getUserById', idUser)
      this.USERCHOOSE = this.user
      console.log(this.USERCHOOSE)

    },
    async updateUser() {
      let update = await this.$store.dispatch('user/UpdateUser', this.USERCHOOSE);
      if (!false) {
        await  swal.fire(
                'Good job!',
                'You clicked the button!',
                'success'
        )
        this.$router.push('/app/user/index')
      }
      console.log(update)
      return update
    },
  }
}
</script>

<style scoped>

</style>
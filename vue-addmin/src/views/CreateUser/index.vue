<template>
    <v-container>
      <div class="container flex flex-col justify-center items-center mx-auto " >
        <div
                style="background-image: url()"
                class=" bg-blue-300 h-64 w-24 min-w-full
                rounded-lg shadow-md bg-cover bg-center"
        >
        </div>
        <div class="w-full lg:w-8/12 px-7 -mt-24 justify-center ">
          <div class="relative flex flex-col min-w-0 break-words  mb-6 shadow-lg rounded-lg bg-gray-200 border-0">
            <div class="rounded-t bg-white mb-0 px-6 py-6">
              <div class="text-center flex justify-between">
                <h6 class="text-gray-800 text-xl font-bold">Create User</h6>
                <v-btn
                        @click="createUser()"
                        class="ma-2"
                        outlined
                        color="indigo"
                >
                  Create
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
                              v-model=" form.first_name"
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
                              v-model=" form.last_name"
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
                        Username
                      </label>
                      <input
                              v-model=" form.username"
                              type="text"
                              class="px-3 py-3 placeholder-gray-400 text-gray-700 bg-white rounded text-sm shadow focus:outline-none focus:shadow-outline w-full ease-linear transition-all duration-150"
                              value="Lucky"
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
                              v-model=" form.email"
                              type="text"
                              class="px-3 py-3 placeholder-gray-400 text-gray-700 bg-white rounded text-sm shadow focus:outline-none focus:shadow-outline w-full ease-linear transition-all duration-150"
                              value="Jesse"
                      />
                    </div>
                  </div>
                </div>
                <hr class="mt-6 border-b-1 border-gray-400" />
                <h6 class="text-gray-500 text-sm mt-3 mb-6 font-bold uppercase">
                  Password setting
                </h6>
                <div class="flex flex-wrap">
                  <div class="w-full lg:w-6/12 px-4">
                    <div class="relative w-full mb-3">
                      <label
                              class="block uppercase text-gray-700 text-xs font-bold mb-2"
                              htmlFor="grid-password"
                      >
                        Password
                      </label>
                      <input
                              v-model="form.password"
                              type="password"
                              class="px-3 py-3 placeholder-gray-400 text-gray-700 bg-white rounded text-sm shadow focus:outline-none focus:shadow-outline w-full ease-linear transition-all duration-150"
                              value="Jesse"
                      />
                    </div>
                  </div>
                  <div class="w-full lg:w-6/12 px-4">
                    <div class="relative w-full mb-3">
                      <label
                              class="block uppercase text-gray-700 text-xs font-bold mb-2"
                              htmlFor="grid-password"
                      >
                        Confirm password
                      </label>
                      <input
                              v-model=" form.password_confirm"
                              type="password"
                              class="px-3 py-3 placeholder-gray-400 text-gray-700 bg-white rounded text-sm shadow focus:outline-none focus:shadow-outline w-full ease-linear transition-all duration-150"
                              value="Jesse"
                      />
                    </div>
                  </div>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </v-container>

  <!--    <div>-->
  <!--      <v-card>-->
  <!--        <v-card-title primary-title>-->
  <!--          <h2 class="t-text-2xl  t-text-bold">-->
  <!--            <v-icon class="t-text-orange-500">mdi-account</v-icon>-->
  <!--            Create User-->
  <!--          </h2>-->
  <!--        </v-card-title>-->
  <!--        <v-card class="">-->
  <!--          <v-layout row>-->
  <!--            <v-flex md4 >-->
  <!--              <v-text-field v-model=" form.first_name" required outlined label="First Name"-->
  <!--                            prepend-inner-icon="mdi-account-card-details" type="text"/>-->
  <!--            </v-flex>-->
  <!--            <v-flex md4 >-->
  <!--              <v-text-field v-model=" form.last_name" class="t-ml-0 md:t-ml-2" required outlined label="Last Name"-->
  <!--                            prepend-inner-icon="mdi-account-card-details" type="text"/>-->
  <!--            </v-flex>-->
  <!--            <v-flex md4 >-->
  <!--              <v-text-field v-model=" form.username" required outlined label="Username"-->
  <!--                            prepend-inner-icon="mdi-account" type="text"/>-->

  <!--            </v-flex>-->
  <!--            <v-flex md4 >-->
  <!--              <v-text-field v-model=" form.email" required outlined label="Email" prepend-inner-icon="mdi-email"-->
  <!--                            type="email"/>-->

  <!--            </v-flex>-->

  <!--            <v-flex md4>-->
  <!--              <v-text-field v-model=" form.password" required outlined label="Password" type="password"/>-->
  <!--            </v-flex>-->

  <!--            <v-flex md4>-->
  <!--              <v-text-field v-model=" form.password_confirm" class="t-ml-0 md:t-ml-2" required outlined-->
  <!--                            label="Confirm password" type="password"/>-->
  <!--            </v-flex>-->


  <!--          </v-layout>-->
  <!--          &lt;!&ndash;        <v-checkbox label="ตั้งค่าเป็นแอดมิน" v-model="is_staff" @click="addToAdmin()"></v-checkbox>&ndash;&gt;-->

  <!--          <v-card-actions>-->
  <!--            <div class="t-w-full">-->
  <!--              <v-btn class="t-float-right" large dark @click="createUser()" color="primary">-->
  <!--                <v-icon>mdi-account-add-outline</v-icon>-->
  <!--                สร้างผู้ใช้-->
  <!--              </v-btn>-->
  <!--            </div>-->
  <!--          </v-card-actions>-->
  <!--        </v-card>-->

  <!--      </v-card>-->
  <!--    </div>-->

</template>

<script>
import {call, sync} from 'vuex-pathify'
import swal from 'sweetalert2'

export default {
  name: "index",
  data: () => ({

    form: {
      first_name: null,
      last_name: null,
      username: null,
      password: null,
      password_confirm: null,
      email: null,
    }
  }),
  computed: {},
  mounted() {

  },
  methods: {
    ...call('user/*'),
    async createUser() {
      let data = await this.$store.dispatch('user/createUser', this.form)
      if (data) {
        await  swal.fire(
                'Success!',
                'You clicked the button!',
                'success'
        )
        await this.$router.push('/app/user/index')
      }

      console.log(this.form)
      return data
    },

    async addToAdmin(){
      this.is_staff = true
    }
  }
}
</script>

<style scoped>

</style>
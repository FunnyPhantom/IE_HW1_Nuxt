<template>
  <v-container fluid fill-height>
    <v-layout align-center justify-center>
      <v-flex xs12 md8 lg6>
        <v-card elevation="12">
            <v-layout wrap fill-height style="min-height: 20vh">
              <v-flex xs12 sm8>
                <template v-if="currentAuthState === authStates.register">
                  <div class="pl-2 pt-4">
                    <v-text-field v-for="(item, index) in registerDataArray" :key="index" :label="item.label" :prepend-icon="item.prependIcon" color="info"></v-text-field>
                  </div>
                  <v-layout justify-center>
                    <v-flex xs12 sm8 class="px-2">
                      <v-btn color="primary" block>
                        ثبت نام
                      </v-btn>
                    </v-flex>
                  </v-layout>
                  <v-layout justify-center>
                    <v-flex xs12 sm8 class="px-2">
                      <v-btn color="white" block>
                        <span class="google-button__icon"><svg viewBox="0 0 366 372" xmlns="http://www.w3.org/2000/svg"><path d="M125.9 10.2c40.2-13.9 85.3-13.6 125.3 1.1 22.2 8.2 42.5 21 59.9 37.1-5.8 6.3-12.1 12.2-18.1 18.3l-34.2 34.2c-11.3-10.8-25.1-19-40.1-23.6-17.6-5.3-36.6-6.1-54.6-2.2-21 4.5-40.5 15.5-55.6 30.9-12.2 12.3-21.4 27.5-27 43.9-20.3-15.8-40.6-31.5-61-47.3 21.5-43 60.1-76.9 105.4-92.4z" id="Shape" fill="#EA4335"/><path d="M20.6 102.4c20.3 15.8 40.6 31.5 61 47.3-8 23.3-8 49.2 0 72.4-20.3 15.8-40.6 31.6-60.9 47.3C1.9 232.7-3.8 189.6 4.4 149.2c3.3-16.2 8.7-32 16.2-46.8z" id="Shape" fill="#FBBC05"/><path d="M361.7 151.1c5.8 32.7 4.5 66.8-4.7 98.8-8.5 29.3-24.6 56.5-47.1 77.2l-59.1-45.9c19.5-13.1 33.3-34.3 37.2-57.5H186.6c.1-24.2.1-48.4.1-72.6h175z" id="Shape" fill="#4285F4"/><path d="M81.4 222.2c7.8 22.9 22.8 43.2 42.6 57.1 12.4 8.7 26.6 14.9 41.4 17.9 14.6 3 29.7 2.6 44.4.1 14.6-2.6 28.7-7.9 41-16.2l59.1 45.9c-21.3 19.7-48 33.1-76.2 39.6-31.2 7.1-64.2 7.3-95.2-1-24.6-6.5-47.7-18.2-67.6-34.1-20.9-16.6-38.3-38-50.4-62 20.3-15.7 40.6-31.5 60.9-47.3z" fill="#34A853"/></svg></span>
                        <span class="">
                        ورود با گوگل
                      </span>
                      </v-btn>
                    </v-flex>
                  </v-layout>
                </template>
                <template v-else-if="currentAuthState === authStates.login">

                </template>
              </v-flex>
              <v-flex xs12 sm4 class="primary">
                <!-- todo: separating small and big devices-->
                <template v-if="true">
                  <v-layout justify-center>
                    <v-flex class="text-xs-center py-3">
                      <v-avatar color="rgb(0,0,0,0.24)"  size="100">
                        <v-icon size="80" color="white">
                          school
                        </v-icon>
                      </v-avatar>
                    </v-flex>
                  </v-layout>
                  <v-container fluid class="text-xs-center px-3 pb-5">
                    <v-layout>
                      <v-flex>
                        <p class="title white--text iran-sans-enforce-font">
                          {{ computedAuthText.title }}
                        </p>
                      </v-flex>
                    </v-layout>
                    <v-layout>
                      <v-flex>
                        <div class="subheading white--text iran-sans-enforce-font">
                          {{ computedAuthText.subtitle }}
                        </div>
                      </v-flex>
                    </v-layout>
                    <v-layout>
                      <v-flex>
                        <v-btn icon dark color="black" @click="computedAuthText.buttonFunction()">
                          <v-icon color="white">
                            {{ computedAuthText.icon }}
                          </v-icon>
                        </v-btn>
                      </v-flex>
                    </v-layout>
                  </v-container>
                </template>
              </v-flex>
            </v-layout>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  name: 'auth',
  data: () => ({
    registerDataArray: [
      {
        label: 'نام و نام خانوادگی',
        prependIcon: 'perm_identity'
      },
      {
        label: 'ایمیل',
        prependIcon: 'email'
      },
      {
        label: 'رمز عبور',
        prependIcon: 'lock'
      },
      {
        label: 'تکرار رمز عبور',
        prependIcon: 'lock'
      }
    ],
    authStates: {
      register: 0,
      login: 1
    },
    currentAuthState: undefined,
  }),
  methods: {
    changeToLoginState() {
      console.log('sdsad')
      this.currentAuthState = this.authStates.login
    },
    changeToRegisterState() {
      this.currentAuthState = this.authStates.register
      console.log('sfpjdpwo?')
    }
  },
  computed: {
    computedAuthText() {
      let d = {
        title: '',
        subtitle: '',
        icon: '',
        buttonFunction: undefined
      }

      if (this.currentAuthState === this.authStates.login) {
        d.title = 'عضو سایت نیستی؟'
        d.subtitle = 'با کلیک روی فلش، میتونی رایگان ثبت نام کنی!'
        d.icon = 'chevron_left'
        d.buttonFunction = this.changeToRegisterState
      }
      else if (this.currentAuthState === this.authStates.register) {
        d.title = 'قبلا ثبت نام کردی؟'
        d.subtitle = ' کلیک روی قلش میتونی به صفحه ورود رو باز کنی'
        d.icon = 'chevron_right'
        d.buttonFunction = this.changeToLoginState
      }
      return d
    }
  },
  created() {
    this.currentAuthState = this.authStates.register
  }
}
</script>

<style scoped>
  .google-button__icon {
    display: inline-block;
    vertical-align: middle;
    margin: 8px 0 8px 8px;
    width: 18px;
    height: 18px;
    box-sizing: border-box;
  }
</style>

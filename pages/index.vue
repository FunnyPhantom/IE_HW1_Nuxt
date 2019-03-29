<template>
  <v-container>
    <v-layout>
      <v-flex class="py-5">
        <div class="display-1 iran-sans-enforce-font">
          صفحه مورد نظرتو را انتخاب کن:
        </div>
      </v-flex>
    </v-layout>
    <v-layout justify-space-around>
      <v-flex shrink>
        <v-btn outline color="green" large to="/landing">لندینگ</v-btn>
      </v-flex>
      <v-flex shrink>
        <v-btn outline color="green" large to="/auth">ثبت نام/ ورود</v-btn>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    name: 'MainPage',
    layout: 'simple'
  }
</script>

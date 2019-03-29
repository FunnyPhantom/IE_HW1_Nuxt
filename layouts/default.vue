<template>
  <v-app>
    <v-toolbar color="primary" app dark prominent style="z-index: 10">
      <template v-if="searchBarActive">
        <v-layout class="v-toolbar__items" align-center>
          <v-flex align-center>
            <v-text-field
              single-line
              color="white"
              class="px-0"
            >
              <template slot="prepend">
                <v-icon>
                  search
                </v-icon>
              </template>
              <template slot="append-outer">
                <v-icon @click="closeSearchBar()">
                  close
                </v-icon>
              </template>
            </v-text-field>
          </v-flex>
        </v-layout>
      </template>
      <template v-if="!searchBarActive">
        <v-toolbar-side-icon class="hidden-md-and-up" />
        <v-spacer v-if="$vuetify.breakpoint.smOnly" />
        <v-icon size="48">school</v-icon>
        <v-toolbar-title>
          <div class="iran-sans-enforce-font subheading hidden-xs-only"> مکتب خانه دانشگاه شهید بهشتی </div>
        </v-toolbar-title>
        <v-spacer class="hidden-sm-and-down" />
        <v-toolbar-items class="hidden-sm-and-down">
          <v-layout align-center class="v-toolbar__items">
            <template  v-for="(item, index) in mainMenuDataArray">
              <template v-if="index === 0">
                <v-divider :key="'-1devider'" vertical />
              </template>
              <v-flex :key="'item'+index" class="px-2 navbar-btn v-toolbar__items" align-center @click="activateTab(index)" :class="getDynamicClass(index)">
                {{ item.name }}
              </v-flex>
              <v-divider :key="'divider'+index" vertical />
            </template>
          </v-layout>
        </v-toolbar-items>
        <v-spacer />
        <v-toolbar-items>
          <v-divider vertical />
          <v-layout align-center class="v-toolbar__items">
            <v-flex class="v-toolbar__items px-3 navbar-btn" @click="openSearchBar()">
              <v-icon class="font-weight-bold" medium>
                search
              </v-icon>
            </v-flex>
          </v-layout>
          <v-divider vertical />
          <v-avatar color="white" size="55" class="ma-1">
            <v-img src="https://picsum.photos/100?image=1005" />
          </v-avatar>
          <v-divider vertical />
        </v-toolbar-items>
      </template>
    </v-toolbar>
    <v-toolbar app color="white" height="100" scroll-off-screen :scroll-threshold="70">
      <v-layout align-end class="v-toolbar__items text-xs-center pb-1">
        <v-flex v-for="i in 4" :key="i">
          <v-btn block depressed color="transparent">
            {{ 'لورم ' + mainMenuDataArray[selectedMainItemIndex].name }}
          </v-btn>
        </v-flex>
      </v-layout>
    </v-toolbar>
    <v-content>
      <nuxt />
    </v-content>
    <v-footer
      :fixed="true"
      app
    >
      <span>&copy; 2019</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
      heights: {
        mobileLandscape: 48,
        mobile: 56,
        desktop: 64,
        dense: 48
      },
      mainMenuDataArray: [
        {
          name: 'صفحه اصلی'
        },
        {
          name: 'آموزش'
        },
        {
          name: 'بلاگ'
        },
        {
          name: 'دانلود'
        },
        {
          name: 'قوانین'
        },
        {
          name: 'تماس با ما'
        },
        {
          name: 'درباره ما'
        },
      ],
      searchBarActive: false,
      selectedMainItem: '',
      selectedMainItemIndex: 0
    }
  },
  computed: {
    computedContentHeight () {

      if (
        this.$vuetify.breakpoint.mdAndUp
      ) return this.heights.desktop

      if (this.$vuetify.breakpoint.smAndDown &&
        this.$vuetify.breakpoint.width >
        this.$vuetify.breakpoint.height
      ) return this.heights.mobileLandscape

      return this.heights.mobile
    },
  },
  methods: {
    toggleSearchBar() {
      this.searchBarActive = !this.searchBarActive
    },
    openSearchBar() {
      this.searchBarActive = true
    },
    closeSearchBar() {
      this.searchBarActive = false
    },
    activateTab(mainItemIndex) {
      this.selectedMainItemIndex = mainItemIndex
    },
    isActive(i) {
      if (i === this.selectedMainItemIndex) {
        return {
          'item-active': true
        }
      }
      else return {}
    },
    getDynamicClass(i) {
      return {
        ...this.isActive(i)
      }
    }
  }
}
</script>

<style scoped>
  .navbar-btn {
    user-select: none;
  }
  .navbar-btn:hover {
    cursor: pointer;
    background: #388e3c;
    transition-duration: 100ms;
  }
  .navbar-btn:active {
    background: #2e7d32;
  }
  .item-active {
    background: #81c784;
  }
  .item-active:hover {
    background: #81c784;
  }
  .item-active:active {
    background: #81c784;
  }
</style>

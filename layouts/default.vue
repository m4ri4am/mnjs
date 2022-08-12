<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      color="#034b71"
      right
      fixed
      app
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
          color="white"
          class="text-color"
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-right="clipped" fixed app class="custom-nav">
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title v-text="title" />
      <v-col cols="3" class="mt-6">
        <v-text-field
          class="mx-3 hidden-sm-and-down"
          light
          width="100"
          solo
          label="ما الذي تبحث عنه؟"
          append-icon="mdi mdi-card-search-outline"
        ></v-text-field>
      </v-col>
      <v-spacer />
      <div class="custom-icons">
        <v-switch class="mt-5 px-3 custom-switch" inset></v-switch>
        <v-icon>mdi-bell-outline</v-icon>
      </div>

      <div class="customize-info hidden-sm-and-down">
        <p>عبد الله</p>
        <p>01212121212</p>
      </div>
      <v-avatar size="50" class="circular">
        <img
          src="https://th.bing.com/th/id/OIP.0vGTOBbzG5ODKG6RZW3tNQHaJr?w=139&h=182&c=7&r=0&o=5&dpr=1.25&pid=1.7"
        />
      </v-avatar>
    </v-app-bar>
    <v-main>
      <v-container fluid>
        <Nuxt />
      </v-container>
    </v-main>

    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }} MNJS</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: "DefaultLayout",
  data() {
    return {
      clipped: false,
      drawer: true,
      rightDrawer: false,
      fixed: false,
      title: "",
      items: [
        {
          icon: "mdi mdi-chart-bar-stacked",
          title: "الصفحة الرئيسية",
          to: "/",
        },
        {
          icon: "mdi mdi-shopping",
          title: "الطلبات",
          to: "/test",
        },
      ],
      miniVariant: false,
      right: true,
    };
  },
  watch: {
    miniVariant(val) {
      this.$vuetify.breakpoint.smAndDown = val;
    },
    right(val) {
      this.$vuetify.rtl = val;
    },
    theme(val) {
      this.$vuetify.theme.dark = val;
      console.log(val);
      console.log(this.$vuetify.theme.dark);
    },
    deep: true,
  },
  methods: {},
};
</script>
<style scoped>
.container {
  padding: 0 !important;
}
.customize-select-box {
  margin-top: 1%;
}
.custom-nav {
  background-color: #034b71 !important;
}
.customize-info {
  padding: 0.5rem;
}
.customize-info p {
  margin: 0;
  font-weight: 100;
  color: darkgray;
  padding-right: 20px;
}
.custom-icons {
  display: flex;
  align-items: center;
  justify-content: flex-end;
}
.custom-switch {
  margin-bottom: 0;
  margin-top: 10px;
  flex-flow: column-reverse !important;
}
.ltr {
  direction: ltr;
}
.rtl {
  direction: rtl;
}
.v-main {
  background-color: rgb(237, 237, 237) !important;
}
.text-color {
  color: white !important;
}
</style>

<template>
  <v-app>
    <v-app-bar app color="red" dark>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
    </v-app-bar>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant.sync="mini"
      temporary
      absolute
      bottom
    >
      <v-list-item class="px-2">
        <v-list-item-avatar>
          <v-img
            src="https://cdn1.iconfinder.com/data/icons/computer-techologies-outline-free/128/ic_ironman-64.png"
          ></v-img>
        </v-list-item-avatar>

        <v-list-item-title>IronMan</v-list-item-title>

        <v-btn icon @click.stop="mini = !mini">
          <v-icon>mdi-chevron-left</v-icon>
        </v-btn>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense>
        <v-list-item v-for="item in items" :key="item.title" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-content><router-view />
          <v-footer color="red">
        <div class="white--text">V0.0.1</div>
        <v-spacer></v-spacer>
        <div class="white--text">
          &copy; 2020 -
          {{ new Date().getFullYear() }} TK
        </div>
      </v-footer>
    </v-content>
  </v-app>
</template>

<script>
//import Drawer from "@/components/Fragments/Drawers.vue";
export default {
  name: "App",
  components: {
    //Drawer,
  },
  data: () => ({
    drawer: false,
    mini: true,
    items: [
      { title: "テスト1", icon: "mdi-swap-horizontal-bold" },
      { title: "テスト2", icon: "mdi-information" },
      { title: "テスト3", icon: "mdi-format-list-bulleted" },
      { title: "テスト4", icon: "mdi-plus-box-outline" },
      { title: "テスト5", icon: "mdi-delete-outline" },
    ],
  }),
};
</script>

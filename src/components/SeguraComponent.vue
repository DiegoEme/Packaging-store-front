<template>
  <v-app id="inspire">
    <!-- <v-system-bar app>
      <v-spacer></v-spacer>

      <v-icon>mdi-square</v-icon>

      <v-icon>mdi-circle</v-icon>

      <v-icon>mdi-triangle</v-icon>
    </v-system-bar> -->

    <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Dashboard</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
      icon
      class="mr20"
      @click="salir()"
      >
        <v-icon>mdi-logout</v-icon>
        
      </v-btn>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" fixed temporary>
      <v-card class="mx-auto" width="300">
        <v-list>
          <v-list-item :to="{name: home}">
            <v-list-item-icon>
              <v-icon>mdi-home</v-icon>
            </v-list-item-icon>

            <v-list-item-title>Home</v-list-item-title>
          </v-list-item>

          <v-list-group :value="true" prepend-icon="mdi-account-circle">
            <template v-slot:activator>
              <v-list-item-title>Users</v-list-item-title>
            </template>

            <v-list-group :value="true" no-action sub-group>
              <template v-slot:activator>
                <v-list-item-content>
                  <v-list-item-title>Admin</v-list-item-title>
                </v-list-item-content>
              </template>

              <v-list-item v-for="([title, icon, ruta], i) in admins" 
              :key="i" 
              link
              :to="{name: ruta}">
                <v-list-item-title v-text="title"></v-list-item-title>

                <v-list-item-icon>
                  <v-icon v-text="icon"></v-icon>
                </v-list-item-icon>
              </v-list-item>
            </v-list-group>

            <v-list-group
            v-if="this.$store.state.user.rol==='Administrador'"
             no-action sub-group>
              <template v-slot:activator>
                <v-list-item-content>
                  <v-list-item-title>Actions</v-list-item-title>
                </v-list-item-content>
              </template>

              <v-list-item 
              
              v-for="([title, icon, ruta], i) in cruds" 
              :key="i" 
              link
              :to="{name: ruta}">
                <v-list-item-title v-text="title"></v-list-item-title>

                <v-list-item-icon>
                  <v-icon v-text="icon"></v-icon>
                </v-list-item-icon>
              </v-list-item>
            </v-list-group>
          </v-list-group>
        </v-list>
      </v-card>
    </v-navigation-drawer>

    <v-main class="grey lighten-2">
      <v-container>
        <router-view />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>


export default {
  name: "SeguraComponent",

  components: {
    
  },

  data: () => ({
    drawer: null,
    admins: [
      ["Categoria", "mdi-account-multiple-outline", "Categoria"],
      ["Articulos", "mdi-cog-outline", "Articulo"],
    ],
    cruds: [["Usuarios", "mdi-plus-outline", "Usuario"]],
  }),

  created(){
    this.$store.dispatch('autoLogin');
  },
  methods: {
    salir(){
      this.$store.dispatch('salir');
    }
  }
};
</script>

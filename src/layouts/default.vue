<template>
  <v-app>
    <v-layout class="rounded rounded-md">
      <v-app-bar>
        <v-app-bar-nav-icon variant="text" @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
        <v-toolbar-title>Mi pagina web</v-toolbar-title>
        <v-spacer></v-spacer>
      </v-app-bar>

      <v-navigation-drawer
        v-model="drawer"
        :location="$vuetify.display.mobile ? 'bottom' : undefined"
        temporary
      >
        <v-list>
          <v-list-item title="Pagina pro" subtitle="Vuetify"></v-list-item>
          <v-divider></v-divider>
          <v-list-item link to="/" title="Home"></v-list-item>
          <v-list-item link to="/pagina2" title="Pagina 2"></v-list-item>
          <v-list-item link to="/pagina3" title="Pagina 3"></v-list-item>
        </v-list>
      </v-navigation-drawer>

      <v-main class="d-flex align-center justify-center" style="min-height: 300px;">
        <RouterView />
      </v-main>
    </v-layout>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: false,
  }),
}
</script>


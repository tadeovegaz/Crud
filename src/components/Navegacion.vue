<template>
  <v-card>
    <v-navigation-drawer
      
      v-model="drawer"
      :mini-variant.sync="mini"
      app
    >
      <v-list-item class="px-2">
        <v-list-item-avatar>
          <v-img src="https://scontent.fgdl3-1.fna.fbcdn.net/v/t1.6435-9/82672775_2797938216934349_3331476908826165248_n.jpg?_nc_cat=108&ccb=1-5&_nc_sid=174925&_nc_eui2=AeHCfuv_hdpRRPTMOl_QuBBvtOTWCmS9n0y05NYKZL2fTEswXA9XbZGLGXvvJhijkNzt-KBc1CFF7WBivS4bDd28&_nc_ohc=1AZXcljRgMAAX-MAOIa&_nc_ht=scontent.fgdl3-1.fna&oh=f8f646deb341b9b5ea14045fef504706&oe=619B86FD"></v-img>
        </v-list-item-avatar>

        <v-list-item-title>Tadeo Vega</v-list-item-title>

        <v-btn
          icon
          @click.stop="mini = !mini"
        >
          <v-icon>mdi-chevron-left</v-icon>
        </v-btn>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense>
        <v-list-item
          v-for="item in items"
          :key="item.title"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <router-link class="link" :to="`${item.path}`"> 
              {{ item.title }} 
              </router-link>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </v-card>
</template>

<script>
  export default {
    data () {
      return {
        drawer: true,
        items: [
          { title: 'Listado', icon: 'mdi-clipboard-list', path: '/listar'},
          { title: 'Crear Usuario', icon: 'mdi-plus', path: '/crear'},
        ],
        mini: true,
      }
    },
  }
</script>

<style scoped>

.link{
  text-decoration: none;
  color: black;

}

</style>
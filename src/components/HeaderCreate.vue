<template>
  <v-card class="overflow-hidden">
    <v-app-bar
      
      absolute
      color="#72c453"
      dark
      shrink-on-scroll
      scroll-target="#scrolling-techniques-2"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
        ></v-img>
      </template>

    <v-toolbar-title>Crear usuario</v-toolbar-title>
    <br>
    </v-app-bar>
      <v-container style="height: 150px;">
      </v-container>
  </v-card>
</template>

<style scoped>

.cont{
    min-height: calc(100vh - 100px - 70px);
}

</style>
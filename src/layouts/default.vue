<template>
  <v-app>
    <v-toolbar color="primary">
      <v-toolbar-title>Sistema de Cadastro</v-toolbar-title>
      <v-toolbar-action class="mr-2">
        <v-btn text to="/" prepend-icon="mdi-home">Home</v-btn>
        <v-btn text to="/form" prepend-icon="mdi-account">Form</v-btn>
      </v-toolbar-action>
    </v-toolbar>
    <v-main>
      <router-view />
    </v-main>
    <AppFooter />
  </v-app>
</template>

<script setup>
  //
</script>

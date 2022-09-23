<template>
  <q-layout view="hHr LpR lFf">
    <q-header elevated>
      <q-toolbar>
        <q-toolbar-title
          class="text-h3 text-center FontPokemon"
          style="height: 60px"
          >Pokedex</q-toolbar-title
        >
      </q-toolbar>
    </q-header>
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: "MainLayout",
  data() {
    return {};
  },
};
</script>

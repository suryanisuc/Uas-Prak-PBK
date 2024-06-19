<template>
  <q-layout view="hHh lpR fFf">
    <q-header>
      <q-toolbar>
        <q-toolbar-title>
          UAS
        </q-toolbar-title>

        <q-btn flat to="/">Weather Widget</q-btn>
        <q-btn flat to="/portfolio">Portfolio</q-btn>
        <q-btn flat to="/tugas2">Tugas 2</q-btn>
        <q-btn flat to="/tugas3">Tugas 3</q-btn>
        <q-btn flat to="/tugas4">Tugas 4</q-btn>
        <q-btn flat to="/tugas5">Tugas 5</q-btn>
        <q-btn flat to="/tugas6">Tugas 6</q-btn>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view></router-view>
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
}
</script>

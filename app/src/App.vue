<template>
  <q-layout view="lHh lpR fFf" v-if="store.user">
    <Header />
    <q-page-container>
      <router-view class="content"></router-view>
    </q-page-container>
  </q-layout>
  <Auth v-else />
</template>

<script setup>
import { useQuasar } from 'quasar';
import Header from './components/Header.vue';
import Auth from './components/Auth.vue';
import { store } from './store';
import { supabase } from './supabase';

const q = useQuasar();
q.dark.set(true);

store.user = supabase.auth.user();
supabase.auth.onAuthStateChange((_, session) => {
  store.user = session.user;
});
</script>

<style scoped>
.content {
  margin: 0.5em;
}
</style>

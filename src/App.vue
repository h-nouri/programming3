<script setup>
import Header from './components/Header.vue'
</script>

<template>

<Header/>
<RouterView/>
</template>
<style>
html,body,#app{
  margin: 0;
  padding: 0;
  display: block;
  width: 100%;
}
#app{
  max-width: none;
}
</style>
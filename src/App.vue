<template>
  <div id="app">
    <h1 class="title mb-6">Evergreen | Finanzas</h1>
    <AssetCreation @assetCreated="notifyList($event)" />
    <AssetList :newAsset="trigger" />
  </div>
</template>

<script>
import AssetCreation from './components/AssetCreation.vue';
import AssetList from './components/AssetList.vue';

export default {
  name: 'App',
  components: {
    AssetCreation,
    AssetList,
  },
  methods: {
    notifyList() {
      this.trigger++;
    },
  },
  data() {
    return {
      trigger: 0,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px 20%;
}
</style>

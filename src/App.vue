<template>
  <div id="app">
    <tree :tree-data="file_structure"></tree>
  </div>
</template>

<script>
  import Tree from './components/Tree';
  import dataJson from '../public/static/node_modules.json'

  export default {
    data: () => ({
      file_structure: dataJson
    }),
    components: {
      Tree,
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
  margin-top: 60px;
}
</style>

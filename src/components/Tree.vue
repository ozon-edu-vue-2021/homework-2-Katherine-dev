
<template>
  <div class="tree">
    <ul class="tree__list">
      <directory :node="treeData" hasFocus></directory>
    </ul>
  </div>
</template>

<script>
 import Directory from './Directory.vue';

  export default {
    props: {
      treeData: Object
    },
    components: {
      Directory,
    }
  };
</script>

<style lang="less" scoped>
.tree {
  margin-left: 8px;

  &__list {
    list-style: none;
    padding: 0;
  }
}

</style>
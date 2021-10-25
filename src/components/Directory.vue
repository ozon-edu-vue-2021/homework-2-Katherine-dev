<template>
  <li class="node__tree">
    <div
      class="item"
      :class="{
        file__item: node.type == 'file',
        link__item: node.type == 'link',
      }"
    >
      <button
        v-if="node.contents && node.contents.length"
        class="folder__button"
        @click="isExpanded = !isExpanded"
      >
        <i v-if="!isExpanded" class="bi bi-folder-fill"></i>
        <i v-else class="bi bi-folder2-open"></i>
      </button>
     
      <node-item :node="node" />
    </div>
    <div v-if="isExpanded" class="contents">
      <ul class="contents__list" v-if="node.contents && node.contents.length">
        <directory
          v-for="(child, i) in node.contents"
          :node="child"
          :key="i"
          class="child"
        ></directory>
      </ul>
    </div>
  </li>
</template>

<script>
import NodeItem from "./NodeItem.vue"

  export default {
    name: 'directory',
    props: {
      node: Object
    },
    data: () => ({
      isExpanded: false
    }),
    components:{
      NodeItem,
    }
  };
</script> 

<style lang="less" scoped>
.item {
  display: flex;
  justify-content: flex-start;
  margin-left: 8px;
}

.folder {
  &__button {
  margin-right: 18px;
  border: none;
  background: transparent;
  }
}

ul li {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}

li {
  margin-top: 2px;
}

.contents {
  display: flex;

  &__list {
    display: flex;
    flex-direction: column;
  }
}

.child {
  margin-left: 8px;
}

.file {
  &__item {
  user-select: all;
  cursor: cell;
  }
}
</style>
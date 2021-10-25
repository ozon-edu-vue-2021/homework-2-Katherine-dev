<template>
  <li class="node__tree">
    <div
      class="item"
    >
      <i class="icon" 
      @click="expand" 
      :class="iconType"></i>
      <node-item :node="node" />
    </div>
    <div v-if="isExpanded" class="contents">
      <ul class="contents__list" v-if="node.contents && node.contents.length">
        <directory
          v-for="(child, i) in node.contents"
          :node="child"
          :key="node.name + i"
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
    computed: {
      iconType: function () {
        return {
          'bi bi-folder-fill icon__folder': this.node.type === 'directory' && !this.isExpanded,
          'bi bi-folder2-open icon__folder': this.node.type === 'directory' && this.isExpanded,
          'bi bi-file-text': this.node.type === 'file',
          'bi bi-link': this.node.type === 'link'
        }
      },
    },
    methods: {
      expand() {
        if (this.node.type === 'directory') {
          this.isExpanded = !this.isExpanded
        }
      }
    },
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

.icon {
  margin-right: 8px;
  &__folder {
    cursor: pointer;
  }
}

.node {
  &__tree {
    margin-top: 2px;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
  }
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
</style>
<template>
  <li class="node__tree" ref="node__tree">
    <div class="item">
      <button
        v-if="node.type === 'directory'"
        tabindex="0"
        @click="expand"
        ref="button"
        class="folder__button"
        @focus="isFocused = true"
        @blur="isFocused = false"
      >
        <i :class="iconTypeFolder"></i>
      </button>
      <i class="icon" :class="iconType"></i>
      <node-item :node="node" :path="itemPath" />
    </div>
    <div v-if="isExpanded" class="contents">
      <ul class="contents__list" v-if="node.contents && node.contents.length">
        <directory
          v-for="(child, i) in node.contents"
          :node="child"
          :key="node.name + i"
          class="child"
          :parentPath="itemPath"
        ></directory>
      </ul>
    </div>
  </li>
</template>

<script>
import NodeItem from "./NodeItem.vue";
  
  export default {
    name: 'directory',
    props: {
      node: Object,
      parentPath: {
        type: String,
        default: ''
      },
      hasFocus: Boolean,
    },
    data: function() {
      return {
        isExpanded: false,
        isFocused: false,
        itemPath: `${this.parentPath}/${this.node.name}`
      }
    },
    computed: {
      iconType: function () {
        return {
          'bi bi-file-text': this.node.type === 'file',
          'bi bi-link': this.node.type === 'link'
        }
      },
      iconTypeFolder: function () {
        return {
          'bi bi-folder-fill icon__folder': this.node.type === 'directory' && !this.isExpanded && !this.isFocused,
          'bi bi-folder2-open icon__folder': this.node.type === 'directory' && this.isExpanded,
          'bi bi-folder-symlink-fill icon__folder': this.node.type === 'directory' && this.isFocused && !this.isExpanded,
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
    },
    mounted() {
      if (this.hasFocus) {
        this.$refs.button.focus();
      }
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
  &__list {
    display: flex;
    flex-direction: column;
  }
}

.child {
  margin-left: 8px;
}

.folder {
  &__button {
    border: none;
    background-color: transparent;
    padding: 0;
    color: #64b5f6;

    &:focus {
      color: #0d47a1;
      outline: none;
    }
  }
}
</style>
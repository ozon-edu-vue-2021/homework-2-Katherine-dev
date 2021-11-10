<template>
  <div>
    <span
      class="label"
      :class="{
        file__name: node.type == 'file',
        link__name: node.type == 'link',
        directory__name: node.type =='directory'
      }"
      @click="showPath"
      >{{ node.name }}
    </span>
    <span v-if="isShowPath" class="path"> {{ path }} </span>
    <span v-if="node.type === 'link'" class="link"> {{ node.target }}</span>
  </div>
</template>

<script>

  export default {
    props: {
      node: Object,
      path: String
    },
    data: function () {
      return {
        isShowPath: false
      }
    },
    methods: {
      showPath() {
        // показываем путь до файла / папки, исключая ссылки
        if (this.node.type !== "link") {
          this.isShowPath = true;
        }
      }
    }
  };
</script>

<style lang="less" scoped>
.file {
  &__name {
    user-select: all;
    cursor: cell;
  }
}

.directory {
  &__name {
    user-select: all;
    cursor: cell;
  }
}

.path {
  margin-left: 46px;
}

.link {
  margin-left: 16px;
  user-select: all;
  cursor: pointer;

  &__name {
    user-select: all;
    cursor: cell;
  }
}
</style>
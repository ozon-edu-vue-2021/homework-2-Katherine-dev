<template>
  <div>
    <span
      class="label"
      :class="{
        file__name: node.type == 'file',
        link__name: node.type == 'link',
      }"
      >{{ node.name }}</span
    >
    <span v-if="node.type === 'link'" class="link"> {{ node.target }}</span>
  </div>
</template>

<script>

  export default {
    props: {
      node: Object
    },
  };
</script>

<style lang="less" scoped>
.file {
  &__name {
    user-select: all;
    cursor: cell;
  }
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
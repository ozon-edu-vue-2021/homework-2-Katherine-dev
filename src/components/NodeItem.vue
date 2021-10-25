<template>
  <div>
    <i v-if="node.type === 'file'" class="bi bi-file-text"></i>
    <i v-if="node.type === 'link'" class="bi bi-link"></i>
    <span class="label">{{ node.name }}</span>
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

<style scoped>
.link {
  margin-left: 16px;
  user-select: all;
  cursor: cell;
}

i {
  margin-right: 8px;
}
</style>
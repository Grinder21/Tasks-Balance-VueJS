<template>
  <div class="budjet-list-wrap">
    <ElCard :header="header">
      <template v-if="!isEmpty">
        <div class="list-item" v-for="(item, prop) in list" :key="prop">
        <span class="budjet-comment">{{ item.comment }}</span>
        <span class="budjet-value">{{ item.value }}</span>
        <ElButton type="danger" size="mini" @click="deleteItem(item.id)">Delete</ElButton>
      </div>
      </template>
      <ElAlert v-else type="info" :title="emptyTitle" :closable="false" />
    </ElCard>
  </div>
</template>

<script>
export default {
name: "BudjetList",
props: {
  list: {
    type: Object,
    default: () => ({})
  }
},
data: () => ({
  header: 'Budjet List',
  emptyTitle: "Empty List"
}),
computed: {
  isEmpty() {
    return !Object.keys(this.list).length;
  }
},
methods: {
  deleteItem(id) {
    this.$emit("deleteItem", id);
  }
}
};
</script>

<style scoped>
.budjet-list-wrap {
  max-width: 500px;
  margin: auto;
}

.list-item {
  display: flex;
  align-items: center;
  padding: 10px 15px;
}

.budjet-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
}
</style>
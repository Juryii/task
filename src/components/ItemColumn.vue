<template>
  <div class="Item">
    <div v-if="flagEditItem[0] === itemIndex && flagEditItem[1] === columnIndex">
      <input type="text" autofocus v-model="newInputItemTitle" @blur="onBlur" />
    </div>
    <div class="cardNameItem" v-else>
      <p>{{ newInputItemTitle }}</p>
      <div class="icons">
        <i class="fas fa-pen" @click="flagEditItem = [itemIndex, columnIndex]"></i>
        <i class="fas fa-times" @click="deleteElement"></i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ItemColumn",
  props: ["itemColumnTitle", "itemIndex", "columnIndex"],
  data: function() {
    return {
      flagEditItem: "",
      newInputItemTitle: this.itemColumnTitle
    };
  },
  methods: {
    onBlur() {
      if (!this.newInputItemTitle) {
        alert("Поле не может быть пустым");
        return;
      }
      this.$emit("editElementTitle", this.newInputItemTitle, this.itemIndex);
      this.flagEditItem = "";
    },
    deleteElement() {
      this.$emit("deleteItemColumn", this.itemIndex, this.columnIndex);
    }
  }
};
</script>

<style scoped>
.cardNameItem {
  display: flex;
  align-items: center;
  justify-content: space-around;
}
.Item:hover {
  cursor: pointer;
  background-color: #fff;
  border-radius: 5px;
}
</style>

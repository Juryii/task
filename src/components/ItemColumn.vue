<template>
  <v-list>
    <div v-if="flagEditItem[0] === itemIndex && flagEditItem[1] === columnIndex">
      <v-text-field v-model="newInputItemTitle" @blur="onBlur"></v-text-field>
    </div>
    <v-list-item class="cardNameItem" v-else>
      <v-list-item-title>{{ newInputItemTitle }}</v-list-item-title>
      <v-list-item-icon class="icons">
        <i class="fas fa-pen" @click="flagEditItem = [itemIndex, columnIndex]"></i>
        <i class="fas fa-times" @click="deleteElement"></i>
      </v-list-item-icon>
    </v-list-item>
  </v-list>
</template>

<script>
export default {
  name: "ItemColumn",
  props: {
    itemColumnTitle: {
      type: String,
      required: true
    },
    itemIndex: {
      type: String,
      required: true
    },
    columnIndex: {
      type: String,
      required: true
    }
  },
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

<style scoped></style>

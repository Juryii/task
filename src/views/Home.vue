<template>
  <div class="home container">
    <div class="column">
      <Column
        v-for="(column, index) in columns"
        :columnTitle="column.title"
        :columnIndex="index"
        :key="index"
        :cardItems="column.cardItems"
        @editColumnTitle="editColumnTitle"
        @deleteColumn="deleteColumn"
        @editElementTitle="editElementTitle"
        @deleteItemColumn="deleteItemColumn"
        @addNewCardItem="addNewCardItem"
      ></Column>
      <NewColumn @addNewColumn="addNewColumn"></NewColumn>
    </div>
  </div>
</template>

<script>
import { setObj, getObj } from "@/utils/localStorage";
import Column from "@/components/Column";
import NewColumn from "@/components/NewColumn";

export default {
  name: "home",
  mounted: function() {
    if (getObj("columns")) {
      this.columns = getObj("columns");
    } else {
      setObj("columns", []);
    }
  },
  data: function() {
    return {
      columns: []
    };
  },
  components: {
    Column,
    NewColumn
  },
  methods: {
    editColumnTitle(columnTitle) {
      this.columns[columnTitle.index].title = columnTitle.title;
      this.updateStorage();
    },
    deleteColumn(index) {
      this.columns.splice(index, 1);
      this.updateStorage();
    },
    editElementTitle(title, itemIndex, columnIndex) {
      this.columns[columnIndex].cardItems[itemIndex].title = title;
      this.updateStorage();
    },
    deleteItemColumn(itemIndex, columnIndex) {
      this.columns[columnIndex].cardItems.splice(itemIndex, 1);
      this.updateStorage();
    },
    addNewCardItem(args) {
      if (this.columns[args.index].cardItems) {
        this.columns[args.index].cardItems.push({ title: args.title });
      } else {
        this.columns[args.index].cardItems = [{ title: args.title }];
      }
      this.updateStorage();
    },
    addNewColumn(title) {
      this.columns.push({ title: title });
      this.updateStorage();
    },
    updateStorage() {
      setObj("columns", this.columns);
    }
  }
};
</script>
<style scoped>
.container {
  display: block;
  flex-direction: row;
  flex-wrap: nowrap;
}
.column {
  display: flex;
  flex-direction: row;
  margin-left: 50px;
  width: 400px;
}
</style>

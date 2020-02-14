<template>
  <div class="home">
    <div class="row flex-nowrap ma-11 align-start">
      <Column
        v-for="(column, index) in columns"
        :columnTitle="column.title"
        :columnIndex="index"
        :key="index"
        :cardItems="column.cardItems"
        @updateColumn="updateColumn"
        @showModal="updateModal"
      ></Column>
      <ModalItem v-model="dialog" :card="currentCard"></ModalItem>
      <NewColumn @addNewColumn="addNewColumn"></NewColumn>
    </div>
  </div>
</template>

<script>
import { setObj, getObj } from "@/utils/localStorage";
import Column from "@/components/Column";
import NewColumn from "@/components/NewColumn";
import ModalItem from "@/components/ModalItem";

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
      columns: [],
      dialog: false,
      itemIndex: "",
      itemColumn: "",
      currentCard: {}
    };
  },
  components: {
    Column,
    NewColumn,
    ModalItem
  },
  methods: {
    updateColumn(args) {
      switch (args.action) {
        case "update": {
          console.log(this.columns);
          this.columns[args.index] = args.column;
          console.log(this.columns);
          break;
        }
        case "deleteColumn": {
          this.columns.splice(args.index, 1);
          break;
        }
      }
      this.updateStorage();
    },
    addNewColumn(title) {
      this.columns.push({ title: title });
      this.updateStorage();
    },
    updateStorage() {
      setObj("columns", this.columns);
    },
    updateModal(itemIndex, itemColumn) {
      this.itemIndex = itemIndex;
      this.itemColumn = itemColumn;
      this.currentCard = this.columns[itemColumn].cardItems[itemIndex];
      this.dialog = true;
    }
  }
};
</script>
<style scoped>
.home {
  overflow-x: scroll;
}
</style>

<template>
  <div class="home">
    <v-layout>
      <draggable class="list-group" :list="columns" group="columns" @change="log">
        <Column
          v-for="(column, index) in columns"
          :columnTitle="column.title"
          :columnIndex="index"
          :key="index"
          :cardItems="column.cardItems"
          @updateColumn="updateColumn"
          @showModal="updateModal"
        ></Column>
      </draggable>
      <ModalItem
        v-model="dialog"
        :card="currentCard"
        @deleteElement="deleteElement"
        @onSaveElement="onSaveElement"
      ></ModalItem>
      <NewColumn @addNewColumn="addNewColumn"></NewColumn>
    </v-layout>
  </div>
</template>

<script>
import { setObj, getObj } from "@/utils/localStorage";
import Column from "@/components/Column";
import NewColumn from "@/components/NewColumn";
import ModalItem from "@/components/ModalItem";
import draggable from "vuedraggable";

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
    ModalItem,
    draggable
  },
  methods: {
    add: function() {
      this.column.cardItems.push({});
    },
    replace: function() {
      this.column.cardItems = [{}];
    },
    clone: function(el) {
      return {
        title: el.title + " cloned"
      };
    },
    log: function(evt) {
      window.console.log(evt);
    },
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
    },
    deleteElement() {
      this.currentCard = {};
      this.dialog = false;
      this.columns[this.itemColumn].cardItems.splice(this.itemIndex, 1);
      console.log(this.columns[this.itemColumn]);
      this.updateStorage();
    },
    onSaveElement(newCard) {
      this.columns[this.itemColumn].cardItems[this.itemIndex] = newCard;
      this.updateStorage();
    }
  }
};
</script>
<style scoped>
.list-group {
  display: flex;
}
.home {
  overflow-x: scroll;
}
</style>

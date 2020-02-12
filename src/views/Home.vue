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
    }
  }
};
</script>
<style scoped>
  .home{
    overflow-x: scroll;
  }
/*.container {*/
/*  display: block;*/
/*  flex-direction: row;*/
/*  flex-wrap: nowrap;*/
/*}*/
/*.column {*/
/*  display: flex;*/
/*  flex-direction: row;*/
/*  margin-left: 50px;*/
/*  width: 400px;*/
/*}*/
</style>

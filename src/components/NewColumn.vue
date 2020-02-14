<template>
  <div v-if="!newColumninput">
    <button class="btn_new_column" @click="newColumninput = !newColumninput">Добавить новую колонку</button>
  </div>
  <div class="addNewColumn" v-else>
    <v-text-field label="Ввести заголовок списка" v-model="newColumnTitle"></v-text-field>
    <button @click="addNewColumn">Добавить</button>
  </div>
</template>

<script>
export default {
  name: "NewColumn",
  data() {
    return {
      newColumninput: false,
      newColumnTitle: ""
    };
  },
  methods: {
    addNewColumn() {
      if (!this.newColumnTitle) {
        alert("Введите название колонки");
        return;
      }
      this.$emit("addNewColumn", this.newColumnTitle);
      this.newColumnTitle = "";
      this.newColumninput = false;
    }
  }
};
</script>

<style scoped>
.btn_new_column {
  background: rgba(240, 240, 240, 0.54);
  border: 2px dashed #d6d6d6;
  box-sizing: border-box;
  border-radius: 10px;
  margin-left: 30px;
  padding: 24px 50px;
}
.btn_new_column:hover {
  border: 2px solid #e7e7e7;
}
.addNewColumn {
  margin-left: 30px;
}
.addNewColumn button {
  background: rgba(240, 240, 240, 0.54);
  padding: 24px 50px;
}
.addNewColumn button:hover {
  background: rgb(205, 205, 205);
  border-radius: 10px;
}
</style>

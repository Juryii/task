<template>
  <div v-if="!newColumninput">
    <v-btn @click="newColumninput = !newColumninput">Добавить новую колонку</v-btn>
  </div>
  <div class="addNewColumn" v-else>
    <v-text-field label="Ввести заголовок списка" v-model="newColumnTitle"></v-text-field>
    <v-btn @click="addNewColumn">Добавить</v-btn>
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

<style scoped></style>

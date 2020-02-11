<template>
  <div v-if="!newColumninput">
    <button @click="newColumninput = !newColumninput">Добавить новую колонку</button>
  </div>
  <div class="addNewColumn" v-else>
    <input type="text" placeholder="Ввести заголовок списка" v-model="newColumnTitle" /><br />
    <button @click="addNewColumn">Добавить</button>
  </div>
</template>

<script>
export default {
  name: "NewColumn",
  data: function() {
    return {
      newColumninput: false,
      newColumnTitle: ""
    };
  },
  methods: {
    addNewColumn() {
      if (this.newColumnTitle) {
        this.$emit("addNewColumn", this.newColumnTitle);
        this.newColumnTitle = "";
        this.newColumninput = false;
      } else {
        alert("Введите название колонки");
      }
    }
  }
};
</script>

<style scoped></style>

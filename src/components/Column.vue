<template>
  <v-card class="row ma-5" max-width="300" tile>
    <div flat class="cardName">
      <div class="row justify-center align-center" v-if="flagEditColumntitle !== columnIndex">
        <v-card-title>{{ column.title }}</v-card-title>
        <i class="fas fa-pen" @click="flagEditColumntitle = columnIndex"></i>
        <i class="fas fa-times" @click="deleteColumn"></i>
      </div>
      <div v-else>
        <v-text-field v-model="newColumnTitle" autofocus @blur="onBlur"></v-text-field>
      </div>
    </div>
    <ItemColumn
      v-for="(columnItem, key) in cardItems"
      :itemColumnTitle="columnItem.title"
      :itemIndex="key"
      :key="key"
      :columnIndex="columnIndex"
      @editElementTitle="editElementTitle"
      @deleteItemColumn="deleteItemColumn"
    ></ItemColumn>

    <div v-if="flagInputCard === columnIndex">
      <v-text-field label="Введите заголовок для этой карточки" v-model="inputCardItem"></v-text-field>
      <v-btn @click="addNewCardItem">Добавить</v-btn>
    </div>
    <div v-else>
      <v-btn @click="flagInputCard = columnIndex">Добавить еще одну карточку</v-btn>
    </div>
  </v-card>
</template>

<script>
import ItemColumn from "./ItemColumn";
export default {
  name: "Column",
  components: {
    ItemColumn
  },
  props: {
    columnTitle: {
      type: String,
      required: true
    },
    columnIndex: {
      type: Number,
      required: true
    },
    cardItems: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      newColumninput: false,
      newColumnTitle: this.columnTitle,
      inputCardItem: "",
      flagInputCard: "",
      flagEditColumntitle: "",
      column: { title: this.columnTitle, cardItems: this.cardItems }
    };
  },
  watch: {
    columnTitle(value) {
      this.column.title = value;
    }
  },
  methods: {
    updateColumn(action) {
      this.$emit("updateColumn", { index: this.columnIndex, column: this.column, action: action });
    },
    deleteColumn() {
      this.updateColumn("deleteColumn");
    },
    onBlur() {
      this.column.title = this.newColumnTitle;
      this.updateColumn("update");
      this.flagEditColumntitle = "";
    },

    editElementTitle(newTitle, itemIndex) {
      this.column.cardItems[itemIndex].title = newTitle;
      this.updateColumn("update");
    },
    deleteItemColumn(itemIndex) {
      this.column.cardItems.splice(itemIndex, 1);
      this.updateColumn("update");
    },
    addNewCardItem() {
      if (!this.inputCardItem) {
        alert("поле не может быть пустым");
        return;
      }
      this.column.cardItems.push({ title: this.inputCardItem });
      this.updateColumn("update");
      this.inputCardItem = "";
      this.flagInputCard = "";
    }
  }
};
</script>

<style scoped></style>

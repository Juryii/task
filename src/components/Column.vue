<template>
  <div class="CardItem">
    <div class="cardName">
      <div class="cardNameTitle" v-if="flagEditColumntitle !== columnIndex">
        <h3>{{ column.title }}</h3>
        <div>
          <i class="fas fa-pen" @click="flagEditColumntitle = columnIndex"></i>
          <i class="fas fa-times" @click="deleteColumn"></i>
        </div>
      </div>
      <div v-else>
        <input type="text" v-model="newColumnTitle" autofocus @blur="onBlur" />
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
      <input type="text" placeholder="Введите заголовок для этой карточки" v-model="inputCardItem" /> <br />
      <button @click="addNewCardItem">Добавить</button>
    </div>
    <div v-else>
      <button @click="flagInputCard = columnIndex">Добавить еще одну карточку</button>
    </div>
  </div>
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

<style scoped>
.CardItem {
  min-width: 400px;
  margin-top: 25px;
  border: 1px solid black;
  width: 200px;
  border-radius: 10px;
  background-color: #9d9d9e;
  margin-right: 20px;
}
.cardNameTitle {
  display: flex;
  align-items: center;
  justify-content: space-around;
}
.cardName {
  border-bottom: 1px solid black;
}
</style>

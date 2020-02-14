<template>
  <div class="wrap_btn">
    <div class="card_wrapper">
      <div class="cardName" v-if="flagEditColumntitle !== columnIndex">
        <div class="name_column">{{ column.title }}</div>
        <div class="name_column counter_items">{{ column.cardItems.length }}</div>
      </div>
      <div v-else>
        <v-text-field v-model="newColumnTitle" autofocus @blur="onBlur"></v-text-field>
      </div>

      <ItemColumn
        v-for="(columnItem, key) in cardItems"
        :itemColumnTitle="columnItem.title"
        :itemIndex="key"
        :key="key"
        :columnIndex="columnIndex"
        @showModal="showModal"
        @editElementTitle="editElementTitle"
        @deleteItemColumn="deleteItemColumn"
      ></ItemColumn>
    </div>
    <div class="add_new_card" v-if="flagInputCard === columnIndex">
      <v-text-field label="Введите заголовок для этой карточки" v-model="inputCardItem"></v-text-field>
      <button @click="addNewCardItem">Добавить</button>
    </div>
    <div v-else>
      <button class="btn_new_card" @click="flagInputCard = columnIndex">Добавить еще одну карточку</button>
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
    },
    showModal(itemIndex) {
      this.$emit("showModal", itemIndex, this.columnIndex);
    }
  }
};
</script>

<style scoped>
.wrap_btn {
  width: 326px;
  margin-left: 40px;
}
.card_wrapper {
  box-shadow: 1px 3px 10px rgba(210, 210, 210, 0.56), 0px 1px 2px rgba(0, 0, 0, 0.13);
  background: rgba(240, 240, 240, 0.54);
  border-radius: 10px;
}
.cardName {
  display: flex;
  flex-direction: row;
  margin-top: 12px;
  margin-left: 13px;
  margin-bottom: 12px;
}
.name_column {
  font-weight: bold;
  font-size: 18px;
  line-height: 21px;
  color: #727272;
  margin-right: 10px;
}
.counter_items {
  color: #b3b3b3;
}
.btn_new_card {
  width: 100%;
  background: #ffffff;
  border: 1px solid #dddcee;
  box-sizing: border-box;
  border-radius: 4px;
  padding-top: 16px;
  padding-bottom: 16px;
  margin-top: 16px;
  margin-bottom: 20px;
}
.btn_new_card:hover {
  background-color: rgba(240, 240, 240, 0.54);
}
.add_new_card button {
  background: rgba(240, 240, 240, 0.54);
  padding: 24px 60px;

}
.add_new_card button:hover {
  background: rgb(205, 205, 205);
  border-radius: 10px;
}
</style>

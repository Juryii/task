<template>
  <div class="card">
    <div v-if="flagEditItem[0] === itemIndex && flagEditItem[1] === columnIndex">
      <v-text-field v-model="newInputItemTitle" @blur="onBlur"></v-text-field>
    </div>
    <div class="cardNameItem" @click="showModal" v-else>
      <div class="card_title">{{ newInputItemTitle }}</div>
      <span :style="{'background-color': labelss[0].color}">{{ labelss[0].name }}</span>
      <div class="icons">
        <i class="fas fa-pen" @click="flagEditItem = [itemIndex, columnIndex]"></i>
      </div>
      <div class="user_info">
<!--        <div class="user-avatar"><img src="@/assets/resistance.jpg" alt="Аватар"></div>-->
        <div class="user-avatar user-avatar--text">U</div>
        <div>UserName</div>
      </div>
    </div>
  </div>
</template>

<script>
import { labels, members } from "../utils/constans";

export default {
  name: "ItemColumn",
  props: {
    itemColumnTitle: {
      type: String,
      required: true
    },
    itemIndex: {
      type: Number,
      required: true
    },
    columnIndex: {
      type: Number,
      required: true
    }
  },
  data: function() {
    return {
      flagEditItem: "",
      labelss: labels,
      memberss: members,
      newInputItemTitle: this.itemColumnTitle
    };
  },
  methods: {
    onBlur() {
      if (!this.newInputItemTitle) {
        alert("Поле не может быть пустым");
        return;
      }
      this.$emit("editElementTitle", this.newInputItemTitle, this.itemIndex);
      this.flagEditItem = "";
    },
    deleteElement() {
      this.$emit("deleteItemColumn", this.itemIndex, this.columnIndex);
    },
    showModal() {
      this.$emit("showModal", this.itemIndex);
    }
  }
};
</script>

<style scoped>
.cardNameItem {
  font-weight: normal;
  font-size: 16px;
  line-height: 19px;
  color: #0e0e0e;
  background: #ffffff;
  border: 2px solid rgba(245, 25, 25, 0.25);
  box-shadow: 1px 3px 10px rgba(210, 210, 210, 0.56), 0px 1px 2px rgba(0, 0, 0, 0.13);
  border-radius: 6px;
  margin: 8px;
  padding: 16px;

}
.card_title{
  margin-bottom: 16px;
}
  .cardNameItem span{
    border-radius: 3px;
    padding: 4px 8px;
  }
  .user_info{
    margin-top: 15px;
    display: flex;
    align-items: center;
  }
.user-avatar{
  height: 40px;
  width: 40px;
  border-radius: 50%;
  margin-right: 16px;
  box-shadow: -4px -4px 8px #FFFFFF, 4px 4px 8px #ECECEC;
}
.user-avatar--text{
  background-color: #dee5c9;
  line-height: 40px;
  text-align: center;
}

.user-avatar img{
  width: inherit;
  height: inherit;
  object-fit: cover;
  border-radius: inherit;
}
.cardNameItem:hover{
  background: #EDF4FA;
}
.cardNameItem:hover .card_title {
  color: blue;
}
</style>

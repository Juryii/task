<template>
  <div class="card">
    <div v-if="flagEditItem[0] === itemIndex && flagEditItem[1] === columnIndex">
      <v-text-field v-model="newInputItemTitle" @blur="onBlur"></v-text-field>
    </div>
    <div class="cardNameItem" @click="showModal" v-else>
      <div class="card_title">{{ newInputItemTitle }}</div>
      <span v-if="item.labelIndex" :class="'tag--' + labelss[item.labelIndex].tag">{{
        labelss[item.labelIndex].name
      }}</span>
      <span v-else :class="'tag--' + labelss[0].tag">{{ labelss[0].name }}</span>
      <!-- <span :style="{ 'background-color': labelss[0].color }">{{ labelss[0].name }}</span> -->
      <div class="icons">
        <i class="fas fa-pen" @click="flagEditItem = [itemIndex, columnIndex]"></i>
      </div>
      <div class="user_info" v-if="item.memberIndex">
        <div v-if="memberss[item.memberIndex].avatar" class="user-avatar">
          <img src="@/assets/resistance.jpg" alt="Аватар" />
        </div>
        <div v-else class="user-avatar user-avatar--text">{{ memberss[item.memberIndex].name[0] }}</div>
        <div class="user-name-text">{{ memberss[item.memberIndex].name }}</div>
      </div>
      <div class="user_info" v-else>
        <div class="user-avatar user-avatar--text">U</div>
        <div class="user-name-text">UserName</div>
      </div>
    </div>
  </div>
</template>

<script>
import { labels, members } from "../utils/constans";

export default {
  name: "ItemColumn",
  props: {
    item: {
      type: Object,
      required: true
    },
    itemTitle: {
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
      itemElement: this.item,
      newInputItemTitle: this.itemTitle
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
  margin-bottom: 8px;
  padding: 16px;
}
.card_title {
  margin-bottom: 16px;
  overflow-wrap: break-word;
}
.cardNameItem span {
  border-radius: 3px;
  padding: 4px 8px;
}
.user_info {
  margin-top: 15px;
  display: flex;
  align-items: center;
  padding-bottom: 12px;
}
.user-avatar {
  height: 40px;
  width: 40px;
  border-radius: 50%;
  margin-right: 16px;
  box-shadow: -4px -4px 8px #ffffff, 4px 4px 8px #ececec;
}
.user-avatar--text {
  background-color: #dee5c9;
  line-height: 40px;
  text-align: center;
  font-weight: bold;
  font-size: 16px;
}
.user-name-text {
  font-weight: normal;
  font-size: 15px;
  line-height: 18px;
  color: #0e0e0e;
}
.user-avatar img {
  width: inherit;
  height: inherit;
  object-fit: cover;
  border-radius: inherit;
}
.cardNameItem:hover {
  background: #edf4fa;
}
.cardNameItem:hover .card_title {
  color: blue;
}
.card:last-child .cardNameItem {
  margin-bottom: 0;
}
.tag--highest {
  color: #ffffff;
  background-color: #d5495a;
}
.tag--high {
  color: #ffffff;
  background-color: #f0a4ad;
}
.tag--medium {
  color: #b5a15f;
  background-color: #fbf0ca;
}
.tag--low {
  color: #6ca451;
  background-color: #dbf1d1;
}
.tag--lowest {
  color: #388513;
  background-color: #a0ce8b;
}
</style>

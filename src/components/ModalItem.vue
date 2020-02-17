<template>
  <div>
    <v-dialog :value="isOpen" width="710px" @input="onDialogInput">
      <div class="wrapp_modal_window">
        <div class="title_wrap">
          <div class="head_card_title" v-if="!flagEditTitle">
            {{ card.title }}
          </div>
          <div class="edit_title" v-else>
            <v-text-field type="text" v-model="card.title" @blur="flagEditTitle = false" />
          </div>
          <button @click="close"><img src="@/assets/ic-close.svg" alt="Закрыть" /></button>
        </div>
        <div class="change_icons">
          <div class="is_icon" @click="flagEditTitle = true">
            <img src="@/assets/ic-edit.svg" alt="Редактировать заголовок" />
          </div>
          <div @click="deleteElemet" class="is_icon"><img src="@/assets/ic-trash.svg" alt="Удалить элемент" /></div>
        </div>
        <div class="desc_row">
          <div class="description">
            <span class="placeholder_description">Описание задачи</span>
            <v-textarea class="description_text" v-model="descriptionCard" :value="descriptionCard"></v-textarea>
            <!-- <div class="description_text">
              Lorem ipsum dolor sit amet, consectetur adipisicing elit. Facere impedit magnam soluta veritatis voluptas.
              Ad dolorem est modi quisquam sint unde. Consequatur consequuntur ea earum impedit laboriosam maxime nulla
              quas.{{ card.description }}
            </div> -->
            <div class="button_wrapper">
              <button class="btn_save" @click="onSaveElement">Сохранить</button
              ><button class="btn_cancel" @click="close">Отменить</button>
            </div>
          </div>
          <div class="selects_panel">
            <div class="priority">
              <span>Приоритет</span>
              <v-select
                item-text="name"
                v-model="selectedLebel"
                :items="labels"
                :label="card.labelIndex ? labels[card.labelIndex].name : 'select label'"
                solo
              >
              </v-select>
            </div>

            <div class="executor">
              <span>Исполнитель</span>
              <v-select
                item-text="name"
                v-model="selectedMember"
                :items="members"
                :label="card.memberIndex ? members[card.memberIndex].name : 'select user'"
                solo
              ></v-select>
            </div>
          </div>
        </div>
      </div>
    </v-dialog>
  </div>
</template>

<script>
import { labels, members } from "../utils/constans";

export default {
  name: "ModalItem",
  props: {
    card: {
      type: Object,
      default: () => {}
    },
    value: Boolean
  },
  data() {
    return {
      flagEditTitle: false,
      isOpen: this.value,
      members: members,
      labels: labels,
      currentCurd: {},
      descriptionCard: this.card.description,
      selectedMember: this.card.memberIndex,
      selectedLebel: this.card.labelIndex
    };
  },
  watch: {
    value(value) {
      this.isOpen = value;
    }
  },
  methods: {
    clearVars() {
      this.currentCurd = {};
      this.descriptionCard = "";
      this.selectedMember = "";
      this.selectedLebel = "";
    },
    deleteElemet() {
      this.$emit("deleteElement");
    },
    onDialogInput(val) {
      val ? this.open() : this.close();
    },
    close() {
      this.isOpen = false;
      this.$emit("input", false);
    },
    open() {
      this.isOpen = true;
      this.clearVars();
      this.$emit("input", true);
    },
    onSaveElement() {
      if (this.selectedLebel) {
        let labelIndex = labels.findIndex(label => label.name === this.selectedLebel);
        if (labelIndex == -1) {
          return;
        }
        this.currentCurd.labelIndex = labelIndex;
      }
      if (this.selectedMember) {
        let memberIndex = members.findIndex(member => member.name === this.selectedMember);
        if (memberIndex == -1) {
          return;
        }
        this.currentCurd.memberIndex = memberIndex;
      }
      if (this.descriptionCard) {
        this.currentCurd.description = this.descriptionCard;
      } else {
        this.currentCurd.description = this.card.description;
      }
      this.currentCurd.title = this.card.title;
      console.log(this.currentCurd);
      this.$emit("onSaveElement", this.currentCurd);
      this.close();
      this.clearVars();
    }
  }
};
</script>

<style scoped>
.wrapp_modal_window {
  background-color: #fff;
}
.title_wrap {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-right: 24px;
}
.change_icons {
  display: flex;
  align-items: center;
  margin-left: 24px;
}
.is_icon {
  width: 24px;
  height: 24px;
  margin-right: 8px;
  background: #edf4fa;
  border-radius: 4px;
}
.is_icon img {
  width: inherit;
  height: inherit;
  object-fit: cover;
  border-radius: inherit;
}
.is_icon:hover {
  background: #d8e8f8;
}
.head_card_title {
  font-weight: bold;
  font-size: 24px;
  line-height: 28px;
  color: #0e0e0e;
  margin: 24px 24px 12px 24px;
  padding-top: 24px;
}
.description {
  width: 492px;
  margin-left: 24px;
  margin-right: 12px;
  background-color: #bfbfbf;
  margin-top: 36px;
}
.placeholder_description {
  margin-top: 12px;
  margin-left: 18px;
  font-size: 11px;
  line-height: 13px;
  color: #727272;
}
.description_text {
  margin-left: 18px;
  margin-right: 18px;
}
.button_wrapper {
  font-weight: normal;
  font-size: 15px;
  line-height: 18px;
  padding-top: 17px;
  padding-left: 24px;
  padding-bottom: 26px;
}
.btn_save {
  font-size: 15px;
  line-height: 18px;
  color: #ffffff;
  background: #023cab;
  box-shadow: 0px 1px 12px rgba(148, 177, 235, 0.46), 0px 2px 4px rgba(26, 100, 210, 0.22);
  border-radius: 4px;
  padding: 16px 46px;
  margin-right: 14px;
}
.btn_cancel {
  font-size: 15px;
  line-height: 18px;
  color: #201f40;
  padding: 16px 46px;
  background: #ffffff;
  border: 1px solid #dddcee;
  box-sizing: border-box;
  border-radius: 4px;
}
.desc_row div span {
  font-size: 11px;
  line-height: 13px;
  color: #727272;
  margin-bottom: 5px;
}
.selects_panel {
  margin-left: 24px;
  margin-right: 24px;
  margin-top: 36px;
}

.desc_row {
  display: flex;
}
.edit_title {
  margin-top: 24px;
  margin-left: 24px;
  margin-right: 24px;
  margin-bottom: 12px;
  width: 100%;
}
</style>

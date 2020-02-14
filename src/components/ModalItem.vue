<template>
  <div>
    <v-dialog :value="isOpen" width="710px" @input="onDialogInput">
      <div class="wrapp_modal_window">
        <div class="title_wrap">
          <div class="head_card_title">
            {{ card.title }}
          </div>
          <button @click="close"><img src="@/assets/ic-close.svg" alt="Закрыть" /></button>
        </div>
        <div class="change_icons">
          <div class="is_icon"><img src="@/assets/ic-edit.svg" alt="Редактировать заголовок" /></div>
          <div class="is_icon"><img src="@/assets/ic-trash.svg" alt="Удалить элемент" /></div>
        </div>
        <div class="desc_row">
          <div class="description">
            <span class="placeholder_description">Описание задачи</span>
            <div class="description_text">
              Lorem ipsum dolor sit amet, consectetur adipisicing elit. Facere impedit magnam soluta veritatis voluptas.
              Ad dolorem est modi quisquam sint unde. Consequatur consequuntur ea earum impedit laboriosam maxime nulla
              quas.{{ card.description }}
            </div>
            <div class="button_wrapper">
              <button class="btn_save">Сохранить</button><button class="btn_cancel">Отменить</button>
            </div>
          </div>
          <div class="selects_panel">
            <div class="priority">
              <span>Приоритет</span>
              <v-select :items="labels" label="Solo field" solo> </v-select>
            </div>

            <div class="executor">
              <span>Исполнитель</span>
              <v-select :items="members" label="Solo field" solo></v-select>
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
  mounted() {
    for (let i = 0; i < members.length; i++) {
      this.members.push(members[i].name);
    }
    for (let i = 0; i < labels.length; i++) {
      this.labels.push(labels[i].name);
    }
  },
  props: {
    card: {
      type: Object,
      default: () => {}
    },
    value: Boolean
  },
  data() {
    return {
      isOpen: this.value,
      members: [],
      labels: []
    };
  },
  watch: {
    value(value) {
      this.isOpen = value;
    }
  },
  methods: {
    selects_elem(arr) {
      let select = [];
      for (let i = 0; arr.length < i; i++) {
        select.push(arr[i].name);
      }
      return select;
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
      this.$emit("input", true);
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
  margin-top: 30px;
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
.selects_panel{
  margin-left: 24px;
  margin-right: 24px;
  margin-top: 36px;
}

.desc_row {
  display: flex;
}
</style>

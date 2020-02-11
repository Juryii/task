<template>
    <div class="CardItem">
        <div class="cardName">
<!--          v next line-->
          <div class="cardNameTitle" v-if="flagEditColumntitle !== columnIndex" >
            <h3>{{ columnTitle }}</h3>
            <div>
              <i
                class="fas fa-pen"
                @click="flagEditColumntitle = columnIndex"
              ></i>
              <i
                class="fas fa-times"
                @click="deleteElement(columnIndex)"
              ></i>
            </div>
          </div>
          <div v-else>
          <textarea
            v-model="newColumnTitle"
            cols="30" rows="1"
            autofocus
            @blur="onBlur(columnIndex)"
          ></textarea>
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
<!--        <div class="CardItem" v-for="(columnitem, key) in column.CardItems">-->
<!--          <div  v-if="flagEditItem[0] === key && flagEditItem[1] === columnIndex">-->
<!--            <input-->
<!--              type="text"-->
<!--              autofocus-->
<!--              v-model="columnitem.title"-->
<!--              @blur="editCards('item')"-->
<!--            >-->
<!--          </div>-->
<!--          <div class="cardNameItem" v-else>-->
<!--            <p>{{columnTitle}}</p>-->
<!--            <div>-->
<!--              <i class="fas fa-pen" @click="flagEditItem = [key, columnIndex]"></i>-->
<!--              <i-->
<!--                class="fas fa-times"-->
<!--                @click="deleteElement('item', key, column)"-->
<!--              ></i>-->
<!--            </div>-->
<!--          </div>-->

<!--        </div>-->

        <div v-if="flagInputCard === columnIndex">
          <input
            type="text"
            placeholder="Введите заголовок для этой карточки"
            v-model="inputCardItem"
          > <br>
          <button @click="addNewCardItem(columnIndex)">Добавить</button>
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
    props: [
      'columnTitle',
      'columnIndex',
      'cardItems'
    ],
    data: function () {
      return {
        newColumninput: false,
        newColumnTitle: this.columnTitle,
        inputCardItem: '',
        flagInputCard: '',
        flagEditColumntitle: '',


      }
    },
    components: {
      ItemColumn
    },
    methods: {
      onBlur(columnIndex) {
        this.$emit('editColumnTitle', {title: this.newColumnTitle,index: columnIndex});
        this.flagEditColumntitle = ''
      },
      deleteElement(columnIndex) {
        this.$emit('deleteColumn', {index: columnIndex})
      },
      editElementTitle(title, itemIndex, columnIndex){
        this.$emit('editElementTitle', title, itemIndex, columnIndex)
      },
      deleteItemColumn(itemIndex, columnIndex){
        this.$emit('deleteItemColumn', itemIndex, columnIndex)
      },
      addNewCardItem(columnIndex) {
        if(!this.inputCardItem){
          alert('поле не может быть пустым');
          return
        }
        this.$emit('addNewCardItem', {index: columnIndex, title: this.inputCardItem});
        this.inputCardItem = '';
        this.flagInputCard = ''
      }
    }
  }
</script>

<style scoped>
  .CardItem{
    min-width: 400px;
    margin-top: 25px;
    border: 1px solid black;
    width: 200px;
    border-radius: 10px;
    background-color: #9d9d9e;
    margin-right: 20px;

  }
  .cardNameTitle{
    display: flex;
    align-items: center;
    justify-content: space-around;
  }
  .cardName{
    border-bottom: 1px solid black;
  }
</style>
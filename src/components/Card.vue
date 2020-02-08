<template>
  <div class="container">
    <div class="column" v-for="(column, index) in columns">
      <div class="cardName">
        <div class="cardNameTitle" v-if="flagEditColumntitle !== index">
          <h3>{{ column.title }}</h3>
          <i
            class="fas fa-pen"
            @click="flagEditColumntitle = index"
          ></i>
        </div>
        <div v-else>
          <textarea
            cols="30" rows="1"
            autofocus
            @blur="editCards('title')"
            v-model="column.title"
          >{{column.title}}</textarea>
        </div>

      </div>
      <div class="CardItem" v-for="(columnitem, index) in column.CardItems">
        <div  v-if="flagEditItem === index">
          <input
            type="text"
            autofocus
            v-model="columnitem.title"
            @blur="editCards('item')"
          >
        </div>
        <div class="cardNameItem" v-else>
          <p>{{columnitem.title}}</p>
          <i class="fas fa-pen" @click="flagEditItem = index"></i>
        </div>

      </div>
      <div v-if="flagInputCard === ''">
        <button @click="flagInputCard = index">Добавить еще одну карточку</button>
      </div>
      <div v-else-if="flagInputCard === index">
        <input
          type="text"
          placeholder="Введите заголовок для этой карточки"
          v-model="inputCardItem"
        > <br>
        <button @click="addNewCardItem(index)">Добавить</button>
      </div>
    </div>
    <div v-if="!newColumninput">
      <button @click="newColumninput = !newColumninput">Добавить новую колонку</button>
    </div>
    <div class="addNewColumn" v-else>
      <input
        type="text"
        placeholder="Ввести заголовок списка"
        v-model="newColumnTitle"
      ><br>
      <button @click="addNewColumn(newColumnTitle)">Добавить</button>
    </div>
  </div>

</template>

<script>

  export default {
    name: "Card",
    data: function () {
      return {
        newColumninput: false,
        newColumnTitle: '',
        inputCardItem: '',
        flagInputCard: '',
        flagEditColumntitle: '',
        flagEditItem: '',
        columns: []
      }
    },
    mounted: function () {
      if (localStorage.getObj('columns') !== null ) {
        this.columns = localStorage.getObj('columns');
      } else {
        localStorage.setObj('columns', []);
      }
    },
    methods: {
      addNewColumn(title){
        if(title === '' || title == null){
          alert('Введите название колонки');
        }
        else {
          this.columns.push( {title: title} );
          localStorage.setObj('columns', this.columns);
          this.newColumnTitle = '';
          this.newColumninput = false;
        }
      },
      addNewCardItem(index) {
        if(this.inputCardItem === '') {
          alert('Введите заголовок списка')
        }
        else {
          if (typeof this.columns[index].CardItems !== "undefined") {
            //ключ есть
            this.columns[index].CardItems.push( { title: this.inputCardItem } );
          }else{
            //ключа нет
            this.columns[index].CardItems = [{title: this.inputCardItem}];
          }
          localStorage.setObj('columns', this.columns);
          this.inputCardItem = '';
          this.flagInputCard = ''

        }

      },
      editCards(elem){
        console.log('onblur');
        localStorage.setObj('columns', this.columns);
        if(elem === 'title'){
          this.flagEditColumntitle = '';
        }
        else if(elem === 'item'){
          this.flagEditItem = '';
        }

      }
    }

  }
</script>

<style scoped>
  .container{
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
  }
  .column{
    border: 1px solid black;
    width: 200px;
    border-radius: 10px;
    background-color: #ebecf0;
  }
  .CardItem{
    background-color: #fff;
    border-radius: 20px;
  }
  .cardNameItem:hover, .cardNameTitle:hover{
    cursor: pointer;
  }
  .fa-pen:hover{
    color: #2a84c3;
    font-size: 1.4em;
  }
  
  .cardNameTitle, .cardNameItem{
    display: flex;
    justify-content: space-around;
    align-items: center;
  }
</style>
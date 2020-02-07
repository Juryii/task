<template>
  <div class="container">
    <div class="column" v-for="(column, index) in columns">
      <div class="cardName">
        <h3>{{ column.title }}</h3>
      </div>
      <div class="CardItem" v-for="columnitem in column.CardItems">
        <p>{{columnitem.title}}</p>
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
        columns: [
          {
            title: '\'Список дел\'',
            CardItems: [
              {title: 'title 2', description: 'text description 2'},
              {title: 'title 3', description: 'text description 3'},
              {title: 'title 1', description: 'text description 1'}
            ]

          },
          {
            title: '\'В процессе\'',
            CardItems: [
              {title: 'title 2', description: 'text description 2'},
              {title: 'title 3', description: 'text description 3'},
              {title: 'title 1', description: 'text description 1'}
            ]
          },
          {
            title: '\'готово\'',
            CardItems: [
              {title: 'title 2', description: 'text description 2'},
              {title: 'title 3', description: 'text description 3'},
              {title: 'title 1', description: 'text description 1'}
            ]
          },
        ],
      }
    },
    methods: {
      addNewColumn(title){
        if(title === '' || title == null){
          alert('Введите название колонки');
        } else {
          this.columns.push( {title: title} );
          this.newColumnTitle = '';
          this.newColumninput = false
        }
      },
      addNewCardItem(index) {
        if(this.inputCardItem === '') {
          alert('Введите заголовок списка')
        }
        else {
          if (typeof this.columns[index].CardItems !== "undefined") {
            //ключ есть
            this.columns[index].CardItems.push({title: this.inputCardItem});
          }else{
            //ключа нет
            this.columns[index].CardItems = [{title: this.inputCardItem}];
          }
          this.inputCardItem = '';
          this.flagInputCard = ''
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
</style>
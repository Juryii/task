<template>
  <div class="container">
    <div class="column" v-for="column in colunms">
      <div class="cardName">
        <h3>{{ column.title }}</h3>
      </div>
      <div class="CardItem" v-for="columnitem in column.CardItems">
        <p>{{columnitem.title}}</p>
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
        colunms: [
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
        if(title == '' || title == null){
          alert('Введите название колонки');
        } else {
          this.colunms.push( {title: title} );
          this.newColumnTitle = '';
          this.newColumninput = false
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
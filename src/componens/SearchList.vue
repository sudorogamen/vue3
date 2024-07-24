<template>
  <div class="search_product">
    <form @submit.prevent @submit="searchItem" class="search__form">
      <input class="search_in" type="search">
      <button  type="submit">Поиск</button>
    </form>
  </div>
  <div class="search_products_row">
    <div class="search_Item" v-for="Item in serIteams">
      <div class="item" >
        <img :src = Item.src />
        <div class="item__body">
          <div class="item__tittle">{{ Item.title }}</div>
          <div class="item__text">{{ Item.text }}</div>
          <div class="item__prise">{{ Item.price }} </div>
        </div>
      </div>
    </div>
    </div>
</template>

<script>
export default {
  data(){
    return{
      serIteams:[]
    }
  },
  props:{
    Items:{
      type:Array,
      required: true
    },
  },
  methods:{
    searchItem(){
      let search = document.querySelector('.search_in')
      let inf = search.value
      if (document.querySelector('.search_products_row').innerHTML){
        this.serIteams=[]
        document.querySelector('.search_products_row').classList.remove('active')

      }

      for (let i =0;i<this.Items.length;i++){
        if (this.Items[i].title.toLowerCase().replace(/\s+/g, '').includes(inf.toLowerCase().replace(/\s+/g, '')) && inf!==''){
          this.serIteams.push(this.Items[i])
          document.querySelector('.search_products_row').classList.add('active')
        }
      }
      if (search.closest("form").classList.contains('search_error')){
        search.closest('form').querySelector('.errorLabel').remove()
        search.closest("form").classList.remove('search_error')

      }
      if(!this.serIteams.length && inf!==''  ){
        const errorLable = document.createElement('label')
        errorLable.classList.add('errorLabel')
        errorLable.textContent = 'Товар не найден'
        search.closest('form').append(errorLable)
        search.closest("form").classList.add('search_error')
      }
    }
  }


}
</script>

<style  scoped>

.search_product {
}
.search__form {
  display: flex;
  justify-content: right;
  gap: 10px;
  align-items: center;
}
.search button{
  width: 70px;
  height: 30px;
  background: rgba(238, 238, 238, 1);
  border-radius: 8px;
}
.search_in {
}
.search_products_row {
  border: none;
}
.search_products_row.active {
  border: 1px solid rgba(73, 72, 94, 1) ;
  box-shadow: black 0 0 12px;
  border-radius: 20px;
  padding: 20px 0;
  opacity: 1;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 12px;
  align-items: center;
}



</style>
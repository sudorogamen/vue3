<template>
    <form @submit.prevent @submit="CreateItem"  class="product_form">
      <div  class="inputs tittle"><p>Наименование товара</p>
        <input v-model="Item.title"  class="in"  type="text" placeholder="Введите наименование товара"></div>
      <div class="inputs text"><p>Описание товара</p>
        <textarea v-model="Item.text" class="in"  placeholder="Введите описание товара"></textarea></div>
      <div class="inputs src"><p>Ссылка на изображение товара</p>
        <input v-model="Item.src" class="in"  type="text " placeholder="Введите ссылку"></div>
      <div class="inputs price"><p>Цена товара</p>
        <input v-model="Item.price" class="in"  type="text" placeholder="Введите цену"></div>
      <button class="addItem" type="submit">Добавить товар</button>
      <button class="editItem" type="submit">Изменить товар</button>
    </form>
    <button class="backEdit" @submit.stop @click="backEdit">Отмена</button>

</template>

<script>
export default {
  data(){
    return{



    }

  },
  props:{
    Item:{
      type:Object
    }

  },
  methods:{
    backEdit(){
     this.$emit("backEdit")
    },
    CreateItem(){
      let form = document.querySelector('.product_form')

      function validation(form){
        let result = true

        function removeError(input){
          const parent = input.closest('.inputs')
          if (parent.classList.contains('error')){
            parent.querySelector('label').remove()
            parent.classList.remove('error')
          }
        }
        function createError(input, text){
          const parent = input.parentNode
          const errorLable = document.createElement('label')
          errorLable.classList.add('errorLabel')
          errorLable.textContent = text
          parent.append(errorLable)
          parent.classList.add('error')

          result = false
        }
        form.querySelectorAll('.in').forEach(input => {
          removeError(input)
          if (input.value == ''){createError(input, 'Поле является обязательным')}
        })
        return result
      }
      if (validation(form)){
        if(form.classList.contains('edit')){
          this.$emit('editItem')
        }else {
          let madeItem = {
          }
          madeItem.id = Date.now()
          madeItem.title = this.Item.title
          madeItem.text = this.Item.text
          madeItem.src = this.Item.src
          madeItem.price = this.Item.price
          this.$emit('create', madeItem )

        }


      }


    },


  }


}
</script>

<style scoped>
.inputs{
  display: flex;
  flex-direction: column;
  gap: 4px;
}
form button{
  display: none;
}
.addItem{
  display: block;
}
form.edit .addItem{
  display: none;
}
form.edit .editItem{
  display: block;
}
.backEdit{
  display: none;
}
.backEdit.active{
  display: block;
}



</style>
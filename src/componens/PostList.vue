<template>
  <div class="Item" :id=Item.id v-for="Item in Items">
    <div class="item " >
      <div  class="redact">
        <button @click=edit($event) class="edit">Edit</button>
        <button @click=remove($event) class="rem">X</button>
      </div>
      <img :src = Item.src />
      <div class="item__body">
        <div class="item__tittle">{{ Item.title }}</div>
        <div class="item__text">{{ Item.text }}</div>
        <div class="item__prise">{{ Item.price }} </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  props:{
    Items:{
      type:Array,
      required: true
    },

  },
  methods:{
    edit(event){
        this.$emit('edit',event.target.closest('.Item'))

      },
    remove(event){
      this.$emit('remove',event.target.closest('.Item') )
    },



    }



}
</script>

<style scoped>


.item__body{
  height: 200px;
  display: flex;
  flex-direction: column;
  align-items: start;
  color: rgba(63, 63, 63, 1);
  padding: 0 16px;
}
.item__tittle{
  margin: 16px 0 16px;
  font-size: 20px;
  font-weight: 600;
}
.item__text{
  width: 300px;
  flex: 1 1 auto;
  font-size: 16px;
  font-weight: 400;
}
.item__prise{
  margin-bottom: 24px;
  font-size: 24px;
  font-weight: 600;
}




.rem{
  font-size: 24px;
  width: 35px;
  height: 35px;
  border-radius: 50%;
  background: red;

}
.edit{
  font-size: 14px;
  width: 35px;
  height: 35px;
  border-radius: 50%;
  background: #4ad38a;
}
.redact{
  display: flex;
  align-items: center;
  gap: 10px;
  opacity: 0;
  position: absolute;
  right: 5px;
  top: 5px;
}
.item:hover{
  .redact{
    opacity: 1;

  }

}
</style>
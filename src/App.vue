<template>
  <div class="app">
    <div class="wrapper">
      <div class="conteiner">
        <div class="grid_box">
          <div class="search">
            <SearchList :Items="Items"/>
          </div>
          <div class="made_product ">
            <MadeItem  @create="CreateProduct" :Item="Item" />
          </div>
          <div class="products">
            <Item-list @edit="editItem" @remove="removeItem" :Items="Items"/></div>
        </div>
      </div>
    </div>
  </div>


</template>


<script >
import ItemList from "@/componens/PostList.vue";
import MadeItem from "@/componens/MadePost.vue";
import SearchList from "@/componens/SearchList.vue";



export default {
  components:{
    ItemList,MadeItem,SearchList,
  },
  data(){
    return{
      Item:{
        id:'',
        title:'',
        text:'',
        src:"",
        price:''
      },
      Items:[
        {
          id:1,
          src:'https://i.pinimg.com/originals/88/4d/e8/884de81d29f37619ff17935475764213.jpg' ,
          title: 'Товар из массива 1',
          text: 'Довольно-таки интересное описание товара в несколько строк.',
          price:1111111
        },{
          id:2,
          src:'https://i.pinimg.com/originals/88/4d/e8/884de81d29f37619ff17935475764213.jpg' ,
          title: 'Товар из массива 2',
          text: 'Довольно-таки интересное описание товара в несколько строк.',
          price:1111111
        },{
          id:3,
          src:'https://i.pinimg.com/originals/88/4d/e8/884de81d29f37619ff17935475764213.jpg' ,
          title: 'Товар из массива 3',
          text: 'Довольно-таки интересное описание товара в несколько строк.',
          price:1111111
        },{
          id:4,
          src:'https://i.pinimg.com/originals/88/4d/e8/884de81d29f37619ff17935475764213.jpg' ,
          title: 'Товар из массива 4',
          text: 'Довольно-таки интересное описание товара в несколько строк.' ,
          price:1111111
        },{
          id:5,
          src:'https://i.pinimg.com/originals/88/4d/e8/884de81d29f37619ff17935475764213.jpg' ,
          title: 'Товар из массива 5',
          text: 'Довольно-таки интересное описание товара в несколько строк.',
          price:1111111
        },{
          id:6,
          src:'https://i.pinimg.com/originals/88/4d/e8/884de81d29f37619ff17935475764213.jpg' ,
          title: 'Товар из массива 6',
          text: 'Довольно-таки интересное описание товара в несколько строк.' ,
          price:1111111
        },
        {
          id:7,
          src:'https://i.pinimg.com/originals/88/4d/e8/884de81d29f37619ff17935475764213.jpg' ,
          title: 'Товар из массива 7',
          text: 'Довольно-таки интересное описание товара в несколько строк. ' ,
          price:1111111
        }
      ],


    }

  },
  methods:{
    CreateProduct(madeItem){
      this.Items.push(madeItem)
      document.querySelector('.product_form').classList.remove('active')
      this.Item.title=''
      this.Item.text=''
      this.Item.src=""
      this.Item.price=''

    },
    editItem(Item){
      if(!document.querySelector('.product_form').classList.contains('active')){
        document.querySelector('.product_form').classList.add('active')
        for (let i =0;i<this.Items.length;i++){
          if (this.Items[i].id == Item.id){
            this.Item.id=this.Items[i].id
            this.Item.title=this.Items[i].title
            this.Item.text=this.Items[i].text
            this.Item.src=this.Items[i].src
            this.Item.price=this.Items[i].price
            this.Items.splice(this.Items.indexOf(this.Items[i]),1)

          }
        }
      }




    },
    removeItem(Item){
      for (let i =0;i<this.Items.length;i++){
        if (this.Items[i].id == Item.id){
          this.Items.splice(this.Items.indexOf(this.Items[i]),1)

        }
      }
    }
  },

}
</script>


<style>
* {
  padding: 0;
  margin: 0;
  border: none;
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

/* Links */

a, a:link, a:visited  {
  text-decoration: none;
}

a:hover  {
  text-decoration: none;
}

/* Common */

aside, nav, footer, header, section, main {
  display: block;
}

h1, h2, h3, h4, h5, h6, p {
  font-size: inherit;
  font-weight: inherit;
}

ul, ul li {
  list-style: none;
}

img {
  vertical-align: top;
}

img, svg {
  max-width: 100%;
  height: auto;
}

address {
  font-style: normal;
}

/* Form */

input, textarea, button, select {
  font-family: inherit;
  font-size: inherit;
  color: inherit;
  background-color: transparent;
}

input::-ms-clear {
  display: none;
}

button, input[type="submit"] {
  display: inline-block;
  box-shadow: none;
  background-color: transparent;
  background: none;
  cursor: pointer;
}

input:focus, input:active,
button:focus, button:active,
textarea:focus, textarea:active{
  outline: none;
}

button::-moz-focus-inner {
  padding: 0;
  border: 0;
}

label {
  cursor: pointer;
}

legend {
  display: block;
}

body{
  background: #000;
}
.wrapper {

}

.conteiner {
  box-shadow: #4ad38a 0 0 20px;
  background:rgba(255, 254, 251, 0.8);
  width: 1440px;
  margin: 30px auto ;
}

.grid_box {
  padding:  32px ;
  display: grid;
  grid-template-columns: 284px auto;
  grid-template-rows: minmax(100px , auto) auto ;
  grid-template-areas:
            'made_product search'
            ' made_product products';
  row-gap: 16px;
}

.search{
  padding-left: 40px;
  display: grid;
  grid-template-rows: 50px minmax(0,auto);
  grid-area: search;
}


.made_product {
  padding-top: 100px;
  grid-area:made_product ;
  color: rgba(73, 72, 94, 1);

}
.made_product form{
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.made_product textarea{
  resize: none;
  width: 284px;
  height: 108px;
}
input::placeholder,textarea::placeholder,input,textarea {
  padding: 10px 16px  ;
}

.made_product button{
  font-size: 16px;
  font-weight: 600;
  background: rgba(238, 238, 238, 1);
  height: 36px;
  border-radius: 10px;
}
.error input, .error textarea{
  border: red 1px solid;

}
.error label{
  color: red;
}
.search_error label{
  color: red;
}
.products {
  grid-area: products;
  margin-left: 40px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 16px;
  align-items: center;
}
.wrapper textarea{
  border-radius: 8px;
  background: #fff;
}
.wrapper input{
  border-radius: 8px;
  background: #fff;
  height: 36px;
}


.item {
  overflow: hidden;
  border-radius: 10px;
  position: relative;
  background: #fff;
  width: 332px;
  height: 423px;
}


.item img{
  width: 332px;
  height: 220px;
}


</style>
<template>
  <main>
    <Form :items="todo.items"  @add="handleSubmit"/>
    <Items :items="todo.items"  @delete="handleDelete"/>
  </main>
</template>

<script>
import Form from './components/Form.vue';
import Items from './components/Items.vue';

export default {
  name: 'App',
  components: {
    Form,Items
  },
  data(){
    return{
        todo : {
          items : [],
      },
    }
  },
  mounted(){
    let items = localStorage.getItem("items");
    if(items != null){
       this.todo.items = items.split(",");
    }
  },
  updated(){
    if(this.todo.items.length == 0){
      localStorage.clear();
    }
  },
  methods : {
    handleSubmit(item){
        this.todo.items.push(item);    
        localStorage.setItem("items",this.todo.items);    
    },
    handleDelete(item){
      this.todo.items = this.todo.items.filter(i => {
        return i != item;
      });
      localStorage.setItem("items",this.todo.items);
    }
  }
  
}
</script>

<style>
body{
   margin: 0;
   padding: 0;
}

#app {
   width:100%;
   height:100vh;
   display:flex;
   flex-direction: column;
   justify-content:center;
   align-items:center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>

<template>
  <Form/>
</template>

<script>
import Form from './components/Form.vue';


export default {
  name: 'App',
  components: {
    Form,
  },
  data(){
    return{
        todo : {
          item : "",
          items : [],
          hasError : false,
          msg : "",
      }
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

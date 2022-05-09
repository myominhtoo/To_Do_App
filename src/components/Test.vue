<template>
    <h1 v-if="todo.hasError" class="h6 text-center my-2 text-danger fw-bold">{{ todo.msg }}</h1>
    <main>
        <form action="" class="form w-100" @submit.prevent="handleSubmit">
            <div class="form-group d-flex gap-1 w-100">
                <input type="text" class="form-control w-75" placeholder="Write To Do" ref="item"  v-model="todo.item" />
                <button class="btn btn-sm btn-primary w-25" type="submit">Add</button>
            </div>
        </form>

        <ul class="items">
           <div id="msg" v-if="todo.items.length == 0 || todo.items === ''">There is no to do!</div>
           <div v-if="todo.items.length > 0">
               <li v-for="item in todo.items" :key="item" class="item" v-on:click="handleDelete(item)">{{  item }}</li>
           </div>
        </ul>
    </main>
</template>


<script>
 export default {
     data(){
         return{
            todo : {
                 item : "",
                items : [],
                hasError : false,
                msg : "",
            },
         }
     },
     methods : {
         handleSubmit(){
             if(this.todo.item == ""){
                 this.todo.hasError = true;
                 this.todo.msg = "Must not blank for to do item!";
             }else{
                this.todo.hasError = false;
                this.handleCheck(this.todo.item);
               if(!this.todo.hasError){
                    this.handleStorage(this.todo.item);
                    this.todo.item = "";
                    this.$refs.item.focus();
               }
             }

         },
         handleStorage(item){
             let items = localStorage.getItem("items");
    
                this.todo.items.push(item);
                localStorage.setItem("items",this.todo.items);
         },
         handleCheck(item){
             if(this.todo.items.includes(item)){
                 this.todo.hasError = true;
                 this.todo.msg = "Duplicate inputs!";
             }else{
                 this.todo.hasError = false;
             }
         },
         handleDelete(item){
            if(confirm("Are you sure to delete?")){
                 this.todo.items = this.todo.items.filter(i => {
                    return i !== item;
                });
                localStorage.setItem("items",this.todo.items);
            }
         },
     },
     mounted(){
        this.$refs.item.focus();
         if(localStorage.getItem("items") != null){
             this.todo.items = localStorage.getItem("items").split(",");
         }
     },
     updated(){
         localStorage.clear();
     }
 }
</script>

<style>
    input{
        color:inherit;
    }

    #msg{
        color:red;
        font-size:18px;
        font-weight:bold;
        width:100%;
        height:100%;
        padding:30px;
        text-align: center;
    }

    .items{
        width:100%;
        height:300px;
        max-height:300px;
        overflow:scroll;
        list-style-type:none;
        text-align:left;
        padding:15px 5px;
    }

    .item{
        padding:2px 10px;
        border-radius: 2px;
        box-shadow: 0 0 1.5px rgba(0,0,0,0.75);
        font-weight: bold;
        background:#eee;
        color:inherit;
        margin:10px 3px;
    }

    main{
        width:25%;
    }

    @media(max-width:900px){
        main{
            width:50%;
        }
    }

    @media(max-width:600px){
        main{
            width:75%;
        }
    }

</style>
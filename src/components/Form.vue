<template>
    <h1 v-if="hasError" class="h6 text-center my-2 text-danger fw-bold">{{ msg }}</h1>   
     <form action="" class="form w-100" @submit.prevent="handleSubmit">
        <div class="form-group d-flex gap-1 w-100">
            <input type="text" class="form-control w-75" placeholder="Write To Do" ref="item"  v-model="item" />
            <button class="btn btn-sm btn-primary w-25" type="submit">Add</button>
        </div>
    </form>
</template>

<script>
export default {
    props : ["items"],
    data(){
        return{
            hasError : false,
            msg : "",
            item : "",
        }
    },
    methods : {
        handleSubmit(){
            if(this.item == ""){
                this.hasError = true;
                this.msg = "To do must not be empty!!";
                this.$refs.item.focus();
            }else{
               if(this.handleCheck(this.item)){
                   this.hasError = false;
                   this.$emit("add",this.item);
                   this.$refs.item= "";
                   this.$refs.item.focus();
               }
            }
        },
        handleCheck(item){
           if(this.items.includes(item)){
               this.hasError = true;
               this.msg = "Duplicate Task!!";
               this.$refs.item.focus();
               return false;
           }
           return true;
        },
    },
    mounted(){
        this.$refs.item.focus();
    }
}
</script>

<style>

</style>
<template>
     <ul class="items">
           <div id="msg" v-if="items.length == 0">There is no to do!</div>
           <div v-if="items.length > 0">
               <li v-for="item in items" :key="item" class="item" v-on:click="handleDelete(item)">{{  item }}</li>
           </div>
     </ul>
</template>

<script>
export default {
    props :["items"],
    methods : {
        handleDelete(item){
            this.$emit("delete",item);
        }
    }
}
</script>

<style>

</style>
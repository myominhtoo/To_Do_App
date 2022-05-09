<template>
  <div class="w-50">
    <form action="" id="form" class="form text-start" @submit.prevent="handleSubmit">
        <div class="form-group my-3" >
            <label for="" class="form-label">Email</label>
            <input type="email" class="form-control" v-model="email"/>
        </div>

        <div class="form-group my-3" >
            <label for="" class="form-label">Password</label>
            <input type="password" class="form-control" v-model="password"/>
            <p class="h6 text-danger"  v-show="passwordErrors">{{ passwordErrors }}</p>
        </div>

        <div class="form-group my-3">
            <label for="" class="form-label">Gender</label>
            <div class="d-flex justify-content-center align-items-start  gap-2">
                    <label for="" class="form-label">Male</label>
                    <input type="radio" class="form-check-radio" v-model="gender" value="Male">
                    <label for="" class="form-label">Female</label>
                    <input type="radio" class="form-check-radio" v-model="gender" value="Female">
                    <label for="" class="form-label">Other</label>
                    <input type="radio" class="form-check-radio" v-model="gender" value="Other">
            </div>
        </div>

        <div class="form-group my-5" >
            <label for="" class="form-label">Skills</label>
            <input type="text" class="form-control" v-model="tempSkill" @keyup.alt="addSkills">

            <ul class="my-1 p-3">
                <li class="skill" v-for="skill in skills" :key="skill"><span @click="deleteSkill(skill)">{{ skill }}</span></li>     
            </ul>
        </div>

        <div class="form-group my-2 d-flex gap-2 align-items-center" >
            <input type="checkbox" class="form-select-">
            <p class="h6 text-dark my-1">Accept All terms & conditons.</p>
        </div>

        <button class="btn w-100 btn-primary" type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
export default {
 data(){
   return{
        email : "",
        password : "",
        gender : "",
        tempSkill : "",
        skills : [], 
        terms : false,
        passwordErrors : null,
   }
 },
 methods : {
    addSkills(e){
        if(e.key === "," && this.tempSkill){
          if(!this.skills.includes(this.tempSkill)){
                this.skills.push(this.tempSkill);
                this.tempSkill = "";
          }
            this.tempSkill = "";
        }
    },
    deleteSkill(item){
        this.skills = this.skills.filter(skill => {
            return item != skill;
        })
    },
    handleSubmit(){
        this.passwordErrors = this.password.length > 5 ? "" : "Password must be at least 5 words!";
       if(!this.passwordErrors){
           console.log({
               email : this.email,
               password : this.password,
               skills : this.skills,
               gender : this.gender,
               terms : this.terms,
           })
       }
    }
 }
}
</script>

<style scoped>
div{
    margin:100px auto;
}
.skill{
    padding:5px 15px;
    border:10px;
    background:#eee;
    display:inline;
    margin:10px 5px;
    list-style-type:none;
}
</style>
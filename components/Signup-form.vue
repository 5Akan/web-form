<template>
  <form @submit.prevent= "submitForm">
      <!-- Keyup for firing the addSkill fn -->
      <!--  -->
      <label>Email</label>
      <input type="email" required v-model = "email">
      <!-- v-model directive allows us to track the content within "input" -->

      <label>Password</label>
      <input type="password" required v-model = "password">
      <div v-if= "password_error">
          {{password_error}}
      </div>

      <label>Role</label>
        <select v-model="role">
            <option value="developer">web developer</option>
            <option value="designer">web designer</option>
        </select>
         <div>
            <label>Skills: </label>
            <input type="text" v-model="tempSkills" @keyup.alt = "addSkill" >
            <div v-for = "skill in skills" :key = "skill" class ="pill" @click = "deleteSkill(skill)">
                <!-- Data bind a skill to key which is a unique item(skill) in skills. It is used along side  v-for-->
                {{ skill }}
            </div>
        </div>
        <div class="term">
            <input type="checkbox" required v-model= "terms">
            <label>Accept Terms and Conditions</label>
        </div>
        <button>Submit Form</button>
  </form>
    <p>Email: {{email}}</p>
    <p>Password: {{password}}</p>
    <p>Role: {{role}}</p>
    <p>Check: {{terms}}</p>
    <p>Names: {{name}}</p>
    <p>Skills: {{tempSkills}}</p>
    <p>Updateskills: {{skills}}</p>
</template>
    
<script>
export default {
    data(){
        return{
        email: 'oakanimoh@gmail.com',
        password :'',
        password_error :"",
        role:'designer',
        adding:'',
        terms:false,
        name:[],
        tempSkills:"",
        skills:[],
        role:''
        }
        
    },
    methods:{
            addSkill(e){
            if(e.key === "," && this.tempSkills){
                if(!this.skills.includes(this.tempSkills)){
                   this.skills.push(this.tempSkills); 
                }
                
                this.tempSkills = "";
            }
        },
        deleteSkill(skill){
            if(skill){
                //The reason why we are assigning it to the skills array
                //is because we are updating the skills array with the skills.filter
                //method
                this.skills = this.skills.filter((item)=>{
                    //filter checks the array,if condition is true nothing happens if it is false then it removes item
                    return item !== skill;
                });
                
            }
        },
        submitForm(){
            console.log("Form submitted");
             this.password_error = this.password.length >= 5 ? "": "Your char is less than five";

        }
    }
}
</script>

<style>
form{
    max-width: 420px;
    margin: 10px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius:10px;
}

label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size:0.6rem;
    text-transform:uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input, select{
    display: block;
    padding:10px 6px;
    width:100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}
input[type='checkbox']{
    display: inline-block;
    width: 10px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}
.pill{
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size:12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}
</style>
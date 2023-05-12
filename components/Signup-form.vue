<template>
  <form>
      <!-- Keyup for firing the addSkill fn -->
      <!--  -->
      <label>Email</label>
      <input type="email" required v-model = "email">
      <!-- v-model directive allows us to track the content within "input" -->

      <label>Password</label>
      <input type="password" required v-model = "password">

      <label>Role</label>
        <select v-model="role">
            <option value="developer">web developer</option>
            <option value="designer">web designer</option>
        </select>
         <div>
            <label>Skills: </label>
            <input type="text" v-model="tempSkills" @keyup.alt = "addSkill">
            <div v-for="skill in skills" :key= "skill" class="pill">
                <!-- Data bind a skill to key which is a unique item(skill) in skills. It is used along side  v-for-->
                {{ skill }}
            </div>
        </div>
        <div class="term">
            <input type="checkbox" required v-model= "terms">
            <label>Accept Terms and Conditions</label>
        </div>
        <div>
            <input type="checkbox" value="rabi" v-model = "name">
            <label>Rahbhee</label>
        </div>
        <div>
            <input type="checkbox" value="akan" v-model = "name">
            <label>Akanimoh</label>
        </div>
        <div>
            <input type="checkbox" value="zoro" v-model = "name">
            <label>Zoro</label>
        </div>
       
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
        role:'designer',
        adding:'',
        terms:false,
        name:[],
        tempSkills:"",
        skills:[]
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
</style>
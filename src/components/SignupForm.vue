<template>
  <form @submit.prevent="submitHandler">
    <label>Email:</label>
    <input type="email" required v-model="email">

    <label>Password:</label>
    <input type="password" required v-model="password">
    <div class="error" v-if="passwordMessage">{{passwordMessage}}</div>

    <label>Role:</label>
    <select v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
    </select>

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
    <div v-for="skill in skills" :key="skill" class="pill" @click="deleteSkill(skill)">
       <span>
           {{skill}}
       </span> 
    </div>

    <div>
        <input type="checkbox" v-model="terms" required>
        <label>accept terms and conditions</label>
    </div>

    <div class="submit">
        <button>Sign up an account</button>
    </div>

  </form>

  <p> Email: {{email}}</p>
  <p> Password: {{password}}</p>
  <p> Role: {{role}}</p>
  <p> Terms: {{terms}}</p>
  <!-- <p> Names: {{names}}</p> -->
</template>

<script>
export default {
    data() {
        return {
            email: "",
            password: "",
            role: "designer",
            terms: false,
            names: [],
            tempSkill: "",
            skills:[],
            passwordMessage:""
        }
    }, 
    methods:{
        addSkill(e) {
            if( e.key === "," && this.tempSkill) {
                if(!this.skills.includes(this.tempSkill)){
                    this .skills.push(this.tempSkill);
                } 
                this.tempSkill = "";
            }
        },
        deleteSkill(skill) {
            this.skills = this.skills.filter( s =>  s !== skill)
        },
        submitHandler() {
            this.passwordMessage = this.password.length > 5 ? 
            "" : "your password must be more than 5 character";
            if(!this.passwordMessage){
                console.log(this.email, this.password, this.role, this.terms, this.skills);
            }
        }

    }
}
</script>

<style>
form {
    background: white;
    max-width: 420px;
    border-radius: 20px;
    box-shadow: 1px 1px 10px #ddd;
    margin: 20px auto;
    padding: 40px;
    text-align: left;
}
label {
    color: #aaa;
    display: inline-block;
    margin:25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    font-weight: bold;
    letter-spacing: 1px;
}
input, select {
    width: 100%;
    display: block;
    margin: 20px auto;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: 555;
}
input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative; 
    top: 2px;
}
.pill{
    display: inline-block;
    margin: 10px 10px 0 0;
    border-radius: 20px;
    padding: 6px 12px;
    background: #eee;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
    font-size: 15px;
}
button {
    background: #277BC0;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 20px;
    cursor: pointer;
    margin: 15px 0;
    letter-spacing: 1px;
}
.submit{
    text-align: center;
}
.error{
    color: #ff0068;
    font-size: 0.8em;
    font-weight: bold;
    letter-spacing: 1px;
}
</style>
<template>
  <form @submit.prevent="handleSubmit">
    <label for="">Email</label>
    <input type="email" required v-model="email" />

    <label for="">Password</label>
    <input type="password" required v-model="psw" />
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label for="">Role</label>
    <select v-model="role" required>
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>
    <label for="">skills</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill" />

    <div class="pill" v-for="skill in skills" :key="skill">
      <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>
    <div class="terms">
      <input type="checkbox" required v-model="terms" />
      <label for="">Accept terms and conditions</label>
    </div>
    <div class="submit">
        <button>create an account</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      psw: "",
      role: "",
      terms: false,
      tempSkill: "",
      skills: [],
      passwordError: ''
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
          this.tempSkill = "";
        }
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item;
      });
    },
    handleSubmit(){
        this.passwordError = this.psw.length > 5 ?
        '' : 'password must be at least 6 chars long'
        if (!this.passwordError) {
            console.log('email: ', this.email);
            console.log('password: ',this.psw);
            console.log('role: ', this.role);
            console.log('skills: ', this.skills);
            console.log('terms: ', this.terms);
        }
    }
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  padding: 40px;
  border-radius: 10px;
  text-align: left;
}

label {
  display: inline-block;
  color: #aaa;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}

input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}

input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}

.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
button{
    background-color: #0b6dff;
    border:0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}
.submit{
    text-align: center;
}
.error{
    color: #ff0062;
    margin: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>

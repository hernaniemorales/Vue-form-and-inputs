<template>
    <!-- added an event modifier to prevent the default behavior when we click the submit button-->
  <form @submit.prevent="handleSubmit" action="">
    <label for="">Email: </label>
    <input type="email" required v-model="email">

    <label for="">Password: </label>
    <input type="password" required v-model="password">
    <div class="error" v-if="passwordError">{{ passwordError }}</div>

    <label for="">Role: </label>
    <select v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
    </select>

    <label for="">Skills</label>
    <!-- added an alt event modifier so that the comma should not get displayed together with the skill  -->
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
    <div v-for="skill in skills" :key="skill" class="pill">
        <span @click="deleteSkill(skill)"> {{ skill }} </span>
    </div>
    
    <div class="terms">
        <input type="checkbox" required v-model="terms">
        <label for="">Accepts terms and conditions</label>
    </div>

    <!-- <div>
        <input type="checkbox" value="nanie" v-model="names">
        <label for="">Nanie</label>
    </div>
    <div>
        <input type="checkbox" value="nanie2" v-model="names">
        <label for="">Nanie2</label>
    </div>
    <div>
        <input type="checkbox" value="nanie3" v-model="names">
        <label for="">Nanie3</label>
    </div> -->

    <div class="submit">
        <button>Create an Account</button>
    </div>

  </form>

  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms Accepted: {{ terms }}</p>
  <!-- <p>Names: {{ names }}</p> -->
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: '',
            terms: false,
            // names: [],
            tempSkill: '',
            skills: [],
            // deleteSkill: '',
            passwordError: '',
        }
    },
    methods: {
        addSkill(e) {
            // console.log(e);
            //check if it is a comma and has a value before the comma
            if (e.key === ',' && this.tempSkill) {
                //checks the current skills
                //if the current skills is not already included in tempSkills
                if (!this.skills.includes(this.tempSkill)) {
                    //add that skill into the array
                    this.skills.push(this.tempSkill);
                }
                //then clear out the tempSkill to add another one.
                this.tempSkill = '';
            }
        },
        deleteSkill(skill) {
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        handleSubmit() {
            // console.log('form submitted');
            //validate password
            this.passwordError = this.password.length > 5 ?
             '' : 'Password must be at least 6 chars long'

             if(!this.passwordError) {
                console.log('email ', this.email);
                console.log('password ', this.password);
                console.log('role ', this.role);
                console.log('skills ', this.skills);
                console.log('terms accepted:', this.terms);
             }
        },
    }
}
</script>

<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label {
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6rem;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input, select {
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
    button {
        background: #0b6dff;
        border: 0;
        padding: 10px 20px;
        margin-top: 20px;
        color: white;
        border-radius: 20px;
    }
    .submit {
        text-align: center;
    }
    .error {
        color: #ff0062;
        margin-top: 10px;
        font-size: 0.8em;
        font-weight: bold;
    }
</style>
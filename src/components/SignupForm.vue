<template>
    <form @submit.prevent="handleSubmit">
        <label>Email:</label>
        <input type="email" required="required" v-model="email">

        <label>Password:</label>
        <input type="password" required="required" v-model="password">
        <div v-if="passwordErr" class="error">{{ passwordErr }}</div>

        <label>Role:</label>
        <select v-model="role">
            <option value="web developer">Web Developer</option>
            <option value="web designer">Web Designer</option>
        </select>

        <label>Skills:</label>
        <input type="text" v-model="tempSkill" @keyup="addSkill">
        <div v-for="skill in skills" :key="skill" class="pill">
            <span @click="deleteSkill(skill)">{{ skill }}</span>
        </div>

        <div>
            <input type="checkbox" v-model="terms">
            <label>Terms and Conditions</label>
        </div>

        <div class="submit">
            <button>Create an account</button>
        </div>

    </form>
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: '',
            terms: false,
            tempSkill: '',
            skills: [],
            passwordErr: ''
        }
    },
    methods: {
        addSkill(e) {
            if(e.key === ',' && this.tempSkill){
                if(!this.skills.includes(this.tempSkill)){
                    this.skills.push(this.tempSkill)
                }
                this.tempSkill = ''
            }
        },
        deleteSkill(skill) {
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        handleSubmit(e) {
            this.passwordErr = this.password.length > 5 ? '' : 'Password must be at least 6 chars long'
            console.log('Email: ' + this.email)
            console.log('Password: ' + this.password)
            console.log('Role: ' + this.role)
            console.log('Skills: ' + this.skills)
            console.log('Terms Accepted: ' + this.terms)
        }
    }
}
</script>

<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background-color: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label {
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
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
        margin: 0px 10px 0px 0px;
        position: relative;
        top: 2px;
    }
    .pill {
        display: inline-block;
        margin: 20px 10px 0 0;
        padding: 6px 12px;
        background-color: #eee;
        border-radius: 20px;
        font-size: 12px;
        letter-spacing: 1px;
        font-weight: bold;
        color: #777;
        cursor: pointer;
    }
    button {
        background-color: #0b6dff;
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


<template>
    <div>
        <form @submit.prevent="handleSubmit">
            <h1>Login Form</h1>
            <label for="email">Email</label>
            <input type="text" required v-model="email">

            <label for="password">Password</label>
            <input type="password" required v-model="password">

            <div v-if="passwordError" class="error">
                {{ passwordError }}
            </div>
            
            <label for="role">Role</label>
            <select v-model="role">
                <option value="developer">Web Developer</option>
                <option value="designer">Web Designer</option>
            </select>

            <div>
                <input type="checkbox" v-model="terms" required>
                <label for="terms"> Accept Terms and Conditions</label>
            </div>

            <label for="skills">Skills</label>
            <input type="text" v-model="tempSkill" @keyup.alt="addSkill">

            <div v-for="skill in skills" :key="skill" class="pill" @click="removeSkill(skill)">
                <span>{{ skill }}</span>
            </div>

            <button class="submit">
                Submit
            </button>
        </form>

        <p> Email: {{ email }}</p>
        <p> Password: {{ password }}</p>
        <p> Role: {{ role }}</p>
        <p> Terms Accepted: {{ terms }}</p>
        <p> Skills: {{ skills }}</p>
    </div>
</template>

<script>
    export default{
        data(){
            return{
                email: '',
                password: '',
                role: 'developer',
                terms: false,
                tempSkill: '',
                skills: [],
                passwordError: ''
            }
        },

        methods: {
            addSkill(e){
                console.log(e)
                if (e.key === 'Enter'){
                    if(!this.skills.includes(this.tempSkill)){
                        this.skills.push(this.tempSkill)
                    }
                    this.tempSkill = ''
                }
            },
            removeSkill(skill){
                this.skills.pop(skill)  
            },
            handleSubmit(){
                this.passwordError = this.password.length > 6 ? '' : 'Password must be at least 6 characters'
                console.log(this.passwordError)
            }
        }
    }

</script>

<style>
form {
    color: black;
    max-width: 420px;
    margin: 30px auto;
    background: lightblue;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}

label {
    color: black;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}

input {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: black;
    border-bottom: 1px solid #ddd;
    color: #555;
}

input, select{
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: black;
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

h1{
    color: black;
    margin: 25px 0 15px;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}

p{
    color: black
}
</style>
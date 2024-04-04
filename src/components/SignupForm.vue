<template>
    <form class="form-container" @submit.prevent="handleSubmit">
        <div class="field-container">
            <label for="email">Email</label>
            <input type="email" name="email" id="email" v-model="email">
        </div>

        <div class="field-container">
            <label for="password">Password</label>
            <input type="password" name="password" id="password" v-model="password">
            <p class="error">{{ passwordError }}</p>
        </div>

        <div class="field-container">
            <label for="role">Role</label>
            <select name="role" id="role" v-model="role">
                <option value="default" selected disabled>Select your job role...</option>
                <option value="designer">Web Designer</option>
                <option value="developer">Web Developer</option>
            </select>
        </div>

        <div class="field-container skills">
            <label for="tempSkill">Skill</label>
            <input type="text" name="skill" id="skill" v-model="tempSkill" @keyup="addSkill">
        </div>
        <div v-for="skill in skills" :key="skill" class="pill" @click="removeSkill(skill)">
            <p>{{ skill }}</p>
            <img src="../assets/cancel-24.png" alt="x" class="close-icon">
        </div>

        <div class="field-container terms">
            <input type="checkbox" v-model="agreement">
            <label>Accept Terms and Conditions</label>
        </div>

        <div class="field-container">
            <input type="submit" value="Create an Account" class="submit-btn">
        </div>

<!-- 
        <div class="field-container">
            <input type="checkbox" value="Josh" v-model="name">
            <label>Josh</label>
        </div>

        <div class="field-container">
            <input type="checkbox" value="Shaun" v-model="name">
            <label>Shaun</label>
        </div>

        <div class="field-container">
            <input type="checkbox" value="Sean" v-model="name">
            <label>Sean</label>
        </div> -->
    </form>
    <!-- <p>Email: {{ email }}</p>
    <p>Password: {{ password }}</p>
    <p>Role: {{ role }}</p>
    <p>Agreement: {{ agreement }}</p> -->
    <!-- <p>Name: {{ name }}</p> -->
    <!-- <p>Skills: {{ skills }}</p> -->
</template>

<script>
export default {
    data() {
        return {
            email: null,
            password: null,
            role: "default",
            agreement: false,
            // name: []
            tempSkill: null,
            skills: [],
            passwordError: null
        }
    },

    methods: {
        addSkill(e) {
            if(e.key === "," && this.tempSkill !== ",") {
                if(!this.skills.includes(this.tempSkill.slice(0, -1).toUpperCase())) {
                    this.skills.push(this.tempSkill.slice(0, -1).toUpperCase());
                    console.log(this.skills)
                }
                this.tempSkill = null
            } else if(e.key === "," && this.tempSkill === ",") {
                this.tempSkill = null
            }
        },

        removeSkill(skill) {
            // this.skills.splice(this.skills.indexOf(skill))
            // the skill args isn't mandatory,
            // the code still works without it
            // however, there's a semantic bug with the code
            // fix it later??

            // also another way to do it
            this.skills = this.skills.filter((item) => {
                return skill != item
            })
        },

        handleSubmit() {
            // validate password
            this.passwordError = this.password.length > 4? null: "Password should be at least 5 characters long"

            if(!this.passwordError) {
                console.log(`Email: ${this.email}`)
                console.log(`Password: ${this.password}`)
                console.log(`Role: ${this.role}`)
                console.log(`Skills: ${this.skills}`)
                console.log(`Accept Terms: ${this.agreement}`)
            }
        }
    }
}
</script>

<style scoped>
    .form-container {
        max-width: 700px;
        padding: 50px;
        margin: auto;
        text-align: left;
        background: #fff;
        border-radius: 20px;
    }

    .form-container .field-container {
        width: 100%;
        margin: 50px 0;
    }

    .form-container .field-container label {
        font-size: 14px;
        color: #aaa;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }

    .field-container input, select {
        display: block;
        width: 100%;
        height: 50px;
        border: none;
        border-bottom: 1px solid #ddd;
        box-sizing: border-box;
        color: #555;
        font-size: 16px;
        background: #fff;
    }

    .field-container input[type=checkbox] {
        width: 15px;
        margin-right: 10px;
    }

    .field-container.skills {
        margin-bottom: 15px;
    }

    .pill {
        margin: 0px 15px 10px 0;
        display: inline-flex;
        /* background: green; */
        align-items: center;
        background: #cccccc;
        padding: 5px 25px;
        border-radius: 25px;
        cursor: pointer;
        transition: all ease 300ms;
    }

    .pill p {
        font-weight: bold;
        font-size: 12px;
        letter-spacing: 1.15px;
        color: #444;
    }
    .pill .close-icon {
        display: none;
        transition: all ease-out 300ms;
        margin-left: 10px;
        width: 20px;
        height: 20px;
    }

    .pill:hover {
        opacity: .7
    }

    .pill:hover .close-icon{
        display: inline;
        opacity: .7;
    }

    .field-container.terms {
        margin-top: 0;
        /* background: greenyellow; */
        display: flex;
        /* justify-content: space-between; */
        align-items: center;
    }

    .field-container .submit-btn {
        background: #0000ff;
        color: #fff;
        border-radius: 10px;
        cursor: pointer;
        transition: all ease 300ms;
        /* width: 200px;
        height: 40px; */
        margin: auto;
    }

    .field-container .submit-btn:hover {
        opacity: .7;
        box-shadow: 6px 6px 16px #ccc;
    }

    .error {
        color: #dc143c; /* crimson red */
        font-weight: bold;
        letter-spacing: 1px;
        word-spacing: 1.5px;
    }
</style>
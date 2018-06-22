<template>
    <div class="sign-up">
        <p>Let's create a new account !</p>
        <input type="text" v-model="email" placeholder="Email"><br>
        <input type="password" v-model="password" placeholder="Password"><br>
        <input type="password" v-model="confirmPassword" placeholder="Confirm Password"><br>
        <button v-on:click="signUp">Sign Up</button>
        <span>or <router-link to="/login">go back to login</router-link>.</span>
    </div>
</template>

<script>
import firebase from 'firebase'
export default {
    name: 'signUp',
    data: function() {
        return {
            email: '',
            password: '',
            confirmPassword: ''
        }
    },
    methods: {
        signUp: function() {
            if (this.password === this.confirmPassword && this.password.length > 5) {
                firebase.auth().createUserWithEmailAndPassword(this.email, this.password).then(
                    function(user) {
                        alert('Your account has been created!')
                    },
                    function(err) {
                        alert('Oops. ' + err.message)
                    }
                );
            } else {
                alert("Oops. Passwords don't match. Please enter a valid password.")
            }
        }
    }
}
</script>

<style>
    .signUp {
        margin-top: 40px;
    }
    input {
        margin: 10px 0;
        width: 20%;
        padding: 15px;
    }
    button {
        margin-top: 10px;
        width: 10%;
        cursor: pointer;
    }
    span {
        display: block;
        margin-top: 20px;
        font-size: 11px;
    }
</style>



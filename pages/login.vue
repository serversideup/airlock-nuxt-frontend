<template>
    <div>
        <label class="block">Email</label>
        <input type="text" class="border border-gray-900" v-model="email"/>

        <br>

        <label class="block">Password</label>
        <input type="password" class="border border-gray-900" v-model="password"/>

        <br>
        <br>

        <button v-on:click="login()" class="cursor border border-gray-900 p-2">Login</button>
    </div>
</template>

<script>
export default {
    data(){
        return {
            email: '',
            password: ''
        }
    },

    methods: {
        login(){
            this.$axios.get('/airlock/csrf-cookie', {
                headers: {
                    'X-Requested-With': 'XMLHttpRequest'
                },
                withCredentials: true,
            })
            .then( function(){
                this.$auth.loginWith('local', {
                    data: {
                        email: this.email,
                        password: this.password
                    },
                });
            }.bind(this))
        }
    }
}
</script>
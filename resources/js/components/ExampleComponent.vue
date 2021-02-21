<template>
    <v-app id="inspire">
        <v-main>
            <v-container fluid fill-height>
                <v-layout align-center justify-center>
                    <v-flex xs12 sm8 md4>
                        <v-card class="elevation-12">
                            <v-toolbar dark color="primary">
                                <v-toolbar-title>Login form</v-toolbar-title>
                            </v-toolbar>
                            <v-card-text>
                                <v-form>
                                    <v-text-field
                                        v-model="email"
                                        name="Email"
                                        label="Email"
                                        type="text"
                                    ></v-text-field>
                                    <v-text-field
                                        v-model="password"
                                        name="Password"
                                        label="Password"
                                        type="password"
                                    ></v-text-field>
                                </v-form>
                            </v-card-text>
                            <v-card-actions>
                                <v-spacer></v-spacer>
                                <v-btn color="primary" v-on:click="login">Login</v-btn>
                            </v-card-actions>
                        </v-card>
                    </v-flex>
                </v-layout>
            </v-container>
        </v-main>
    </v-app>
</template>

<script>
export default {
    data: () => ({
        email:'',
        password:'',
        user:''
    }),
    methods: {
        login(){
            var vm=this;
            axios.get('/sanctum/csrf-cookie').then(response => {
                axios.post('/api/login', {'email': this.email, 'password': this.password}).then(response => {
                    if (response.data==1);
                    {
                      vm.getUser();
                    }
                });
            });
        },
        getUser(){
            axios.get('/api/user').then(response =>{
                this.user=response.data;
            })
        }
    }
};
</script>

<style></style>

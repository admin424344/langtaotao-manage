<template>
    <v-app>
        <v-content class="vcontent">
            <v-container fluid fill-height>
                <v-layout align-center justify-center>
                    <v-flex xs12 sm8 md4>
                        <v-card class="elevation-12">
                            <v-toolbar dark color="#008B8B">
                                <v-toolbar-title>浪淘淘(LangTaoTao)商城后台管理</v-toolbar-title>
                                <v-spacer></v-spacer>
                            </v-toolbar>
                            <v-card-text>
                                <v-form>
                                    <v-text-field prepend-icon="person" v-model="username" label="用户名" type="text"/>
                                    <v-text-field
                                            prepend-icon="lock"
                                            v-model="password"
                                            label="密码"
                                            id="password"
                                            :append-icon="e1 ? 'visibility' : 'visibility_off'"
                                            :append-icon-cb="() => (e1 = !e1)"
                                            :type="e1 ? 'text' : 'password'"
                                    ></v-text-field>
                                </v-form>
                            </v-card-text>
                            <v-card-actions>
                                <v-spacer></v-spacer>
                                <v-btn color="#008B8B" @click="doLogin">登录</v-btn>
                            </v-card-actions>
                        </v-card>
                    </v-flex>
                </v-layout>
            </v-container>
        </v-content>
        <v-dialog v-model="dialog" width="300px">
            <v-alert icon="warning" color="error" :value="true">
                用户名和密码不能为空
            </v-alert>
        </v-dialog>
    </v-app>
</template>

<script>
    export default {
        data: () => ({
            username: '',
            password: '',
            dialog: false,
            e1: false
        }),
        methods: {
            doLogin() {
                if (!this.username || !this.password) {
                    this.dialog = true;
                    return false;
                }
                let formData = new FormData();
                formData.append("username", this.username)
                formData.append("password", this.password)
                this.$http.post("/auth/login", formData).then(resp => {
                    this.$router.push("/index/dashboard");
                })
            }
        }
    };
</script>
<style>
    .vcontent{
        background-image: url("../assets/login-bg.jpg");
        background-size:cover;
    }
</style>

<template>
  <v-row justify="center">
    <v-col cols="2"></v-col>
    <v-col cols="8">
      <v-flex text-center>
        <v-btn color="primary" @click="googleLogin">
          <v-icon left>mdi-google</v-icon>Googleアカウントでログイン
        </v-btn>
      </v-flex>
      <br />

      <v-text-field type="email" label="メールアドレス" autofocus v-model="email"></v-text-field>

      <v-text-field type="password" label="パスワード" v-model="password"></v-text-field>

      <v-flex text-center>
        <v-btn color="error" @click="signIn">
          <v-icon left>mdi-login</v-icon>ログイン
        </v-btn>
        <br />
        <br />

        <v-btn color="success" :to="{ name: 'SignUp' }">
          <v-icon left>mdi-account-plus</v-icon>新規会員登録はこちらから
        </v-btn>
      </v-flex>
    </v-col>
    <v-col cols="2"></v-col>
  </v-row>
</template>

<script>
import firebase from "firebase/app";
import "firebase/auth";
import { mapActions } from "vuex";

export default {
  data() {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    signIn() {
      firebase
        .auth()
        .signInWithEmailAndPassword(this.email, this.password)
        .then(response => {
          console.log(response);
          this.$router.push({ name: "Todos" });
          this.email = "";
          this.password = "";
        })
        .catch(error => {
          console.log(error);
        });
    },
    ...mapActions(["googleLogin"])
  }
};
</script>

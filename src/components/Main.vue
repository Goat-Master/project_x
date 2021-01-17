<template>
  <v-app class="mainPage">
    <v-container class="container indigo" lighten-2>
      <v-form ref="form">
        <h2 style="color: white">Virtual ATM</h2>
        <v-row>
          <v-spacer></v-spacer>
          <v-text-field
            outlined
            label="Insert Name"
            v-model="name"
            color="white"
            white
            rounded
          ></v-text-field>
          <v-spacer></v-spacer>
        </v-row>
        <v-row>
          <v-spacer></v-spacer>
          <v-text-field
            rounded
            outlined
            color="white"
            label="Insert Pin"
            :rules="numberRules"
            v-model="pin"
          ></v-text-field>
          <v-spacer></v-spacer>
        </v-row>
        <v-row>
          <v-spacer></v-spacer>
          <v-btn @click="submit">Submit</v-btn>
          <v-spacer></v-spacer>
        </v-row>
      </v-form>
    </v-container>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      loginSucessfull: false,
      name: "",
      pin: "",
      numberRules: [
        (v) => /\d/.test(v) || "Coloque números apenas",
        (v) => v.length === 4 || "O pin apenas é composto por 4 algarismos",
      ],
      accounts: [
        {
          name: "zé",
          pin: "1939",
          amount: 1000,
        },
        {
          name: "bruno",
          pin: "1982",
          amount: 9000,
        },
      ],
    };
  },
  methods: {
    submit() {
      if (this.$refs.form.validate()) {
        console.log(this.name + " | " + this.pin);
        for (let i = 0; i <= this.accounts.length; i++) {
          if (
            this.name === this.accounts[i].name &&
            this.pin === this.accounts[i].pin
          ) {
            this.$router.push(this.name);
          }
        }
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
.container {
  margin-top: 20%;
  padding: 30px 30px 30px 30px;
  border-radius: 20px;
}

.mainPage {
  background-image: url('../assets/bg1.jpg');
  background-size: 100% 100%;
  background-attachment: fixed;
  background-repeat: no-repeat;
}
</style>

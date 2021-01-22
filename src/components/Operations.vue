<template>
  <div class="main">
    <h2 class="white display-3 text-uppercase text-center font-weight-black">
      welcome {{ name }}
    </h2>
    <v-container class="container indigo" lighten-2>
      <v-row>
        <v-col>
          <v-btn x-large class="ma-12" @click="withdraw">Withdraw</v-btn>
          <v-btn x-large class="ma-12" @click="deposit">Deposit</v-btn>
          <v-btn x-large class="ma-12" @click="consult"
            >Consult current amount</v-btn
          >
          <v-btn x-large class="ma-12">Transfer</v-btn>
        </v-col>
        <v-col
          ><h3
            v-if="flag"
            class="display-1 text-center"
            style="margin-top: 20%; color: white"
          >
            {{ message }}
          </h3>
          <v-form ref="form" v-if="inp"
            ><v-text-field
              rounded
              outlined
              color="white"
              label="Insert amount"
              v-model="amountInserted"
              :rules="numberRules"
            ></v-text-field>
            <v-btn @click="submit">Submit</v-btn></v-form
          >
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>
<script>
export default {
  props: ["name"],
  data() {
    return {
      numberRules: [(v) => /^\d+$/.test(v) || "Coloque números apenas"],
      amount: 0,
      amountInserted: 0,
      flag: false,
      inp: false,
      with: false,
      message: "",
    };
  },
  methods: {
    withdraw() {
      this.message = "How much would you like to withdraw?";
      this.inp = true;
      this.flag = true;
      this.with = true;
    },
    submit() {
      console.log("submit called " + this.amountInserted);
      if (this.with) {
        if (this.$refs.form.validate()) {
          console.log("amountInserted |||" + this.amountInserted);
          if (this.amountInserted > this.amount) {
            this.message = "You don't have that much money, insert a new value";
          } else {
            this.amount -= this.amountInserted;
            this.message = "Collect your money!";
            this.$refs.form.reset();
            this.inp = false;
          }
        }
      } else {
        if (this.$refs.form.validate()) {
          console.log(this.amountInserted + " || " + this.amount);
          this.amount += parseInt(this.amountInserted);
          this.message = "Deposit sucessfull!";
          console.log(
            `Deposit called. !! ${this.amount} || ${this.amountInserted}`
          );
          this.$refs.form.reset();
          this.inp = false;
        }
      }
    },
    deposit() {
      this.message = "How much would you like to deposit?";
      this.with = false;
      this.inp = true;
      this.flag = true;
    },
    consult() {
      this.message = `Your current amount is ${this.amount}`;
      this.flag = true;
      this.with = false;
      this.input = false;
    },
  },
  created: function () {
    if (this.$route.params.name === "bruno") {
      this.amount = 1000;
    } else {
      this.amount = 100;
    }
  },
};
</script>
<style scoped lang="stylus">
.main {
  background-image: url('../assets/bg1.jpg');
  background-size: 100% 120%;
  background-attachment: fixed;
  background-repeat: no-repeat;
  height: 100vh;
  width: 100%;
}

.container {
  width: 90%;
  height: 90%;
  margin-top: 1%;
  padding: 30px 30px 30px 30px;
  border-radius: 20px;
}

button {
  width: 70%;
}
</style>
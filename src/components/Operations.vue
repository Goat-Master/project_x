<template>
  <div class="main">
    <h2 class="white display-3 text-uppercase text-center font-weight-black">
      welcome {{ name }}
    </h2>
    <v-container class="container" indigo>
      <v-row>
        <v-col>
          <v-btn x-large class="ma-12" @click="withdraw">Withdraw</v-btn>
          <v-btn x-large class="ma-12">Deposit</v-btn>
        </v-col>
        <v-col v-if="flag"
          ><h3
            class="display-1 text-center"
            style="margin-top: 20%; color: white"
          >
            {{ message }}
          </h3></v-col
        >
      </v-row>

      <v-row>
        <v-col>
          <v-btn x-large class="ma-12">Consult current amount</v-btn>
          <v-btn x-large class="ma-12">Transfer</v-btn>
        </v-col>
        <v-col v-if="inp"
          ><v-form ref="form"
            ><v-text-field
              rounded
              outlined
              color="white"
              label="Insert amount"
              v-model="amountInserted"
              :rules="numberRules"
            ></v-text-field>
            <v-btn @click="submit">Submit</v-btn></v-form
          ></v-col
        >
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
      message: "",
    };
  },
  methods: {
    withdraw() {
      this.message = "How much would you like to withdraw?";
      this.inp = true;
      this.flag = true;
    },
    submit() {
      if (this.$refs.form.validate()) {
        if (this.amountInserted > this.amount) {
          this.message = "You don't have that much money, insert a new value";
        } else {
          this.amount = this.amount - this.amountInserted;
          this.message =
            "Collect your money. The amount in your account is now " +
            this.amount;
        }
      }
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
  background-size: 100% 100%;
  background-attachment: fixed;
  background-repeat: no-repeat;
  height: 100vh;
  width: 100%;
}

.container {
  width: 80%;
  height: 80%;
  margin-top: 5%;
}

button {
  width: 40%;
}
</style>
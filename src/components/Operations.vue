<template>
  <div class="main">
    <h2 class="white display-3 text-uppercase text-center font-weight-black">
      welcome {{ name }}
    </h2>
    <v-container class="container">
      <v-row>
        <v-btn x-large class="ma-12">Withdraw</v-btn>

        <v-btn x-large class="ma-12">Deposit</v-btn>
      </v-row>

      <v-row>
        <v-btn x-large class="ma-12">Consult current amount</v-btn>

        <v-btn x-large class="ma-12">Transfer</v-btn>
      </v-row>
    </v-container>
  </div>
</template>
<script>
export default {
  props: ["name"],
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
  width: 60%;
  height: 50%;
  margin-top: 15%;
}

button {
  width: 40%;
}
</style>
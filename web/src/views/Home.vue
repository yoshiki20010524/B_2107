<template>
  <div class="home">
    <div class="logo">
      <img class="logoHead" src="../assets/img/Logo_head.png" />
      <img class="logoName" src="../assets/img/Logo_name.png" />
    </div>

    <div>
      <v-form ref="form" v-model="valid" lazy-validation>
        <v-text-field
          v-model="id"
          :rules="idRules"
          label="Room-id"
          required
        ></v-text-field>

        <v-text-field
          v-model="password"
          :rules="passwordRules"
          label="Room-Password"
          required
        ></v-text-field>
        <v-btn
          depressed
          :disabled="!valid"
          class="mr-4"
          large
          outlined
          color="#000"
          @click="validate"
        >
          ルームに参加する
        </v-btn>
        <v-btn
          depressed
          class="mr-4"
          @click="reset"
          large
          outlined
          color="#000"
        >
          リセット
        </v-btn>
      </v-form>
    </div>
  </div>
</template>
<style scoped>
.home {
  display: grid;
}

.logo {
  max-width: 100%;
  margin-top: 90px;
  margin-bottom: 70px;
}
.logo img {
  width: 220px;
  height: auto;
}

.v-form {
  max-width: 60%;
  height: auto;
  margin-left: auto;
  margin-right: auto;
}
.btn {
  background-color: black;
  color: black;
}
</style>
<script>
export default {
  data: () => ({
    valid: true,
    id: "",
    idRules: [
      (v) => !!v || "Room Id is required",
      (v) => (v && v.length <= 8) || "UnCorrect",
    ],
    password: "",
    passwordRules: [
      (v) => !!v || "Room Password is required",
      (v) => (v && v.length <= 4) || "UnCorrect",
    ],
  }),
  methods: {
    validate() {
      this.$refs.form.validate();
      //画面遷移
      this.$router
        .push({
          name: "Select",
          params: { id: this.id, password: this.password },
        })
        .catch(() => {});
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    },
  },
};
</script>

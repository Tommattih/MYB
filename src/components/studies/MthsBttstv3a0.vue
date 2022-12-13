<template>
  <div class="MtsBase">
    <form id="app-form">
      <input type="text" v-model="input_name" placeholder="Digite seu nome" />
      <input type="number" v-model="input_age" placeholder="Digite sua idade" />
      <input type="submit" value="Enviar" @click="submitForm" />
    </form>
    <p>O meu nome é: {{ name }}, e tenho {{ age }} anos.</p>
    <p>Data binding: {{ input_name }} e {{ input_age }}</p>
  </div>
</template>

<script>
export default {
  name: "MtsBase",
  props: {
    msg: String,
  },
  data() {
    return {
      name: "",
      age: "",
      input_name: "",
      input_age: "",
    };
  },
  methods: {
    submitForm(e) {
      e.preventDefault();
      // console.log("caiu aqui");
      console.log(this.input_name, this.input_age);
      this.name = this.input_name;
      this.age = this.input_age;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
* {
  font-size: 2rem;
  background: #0a1122;
}
</style>

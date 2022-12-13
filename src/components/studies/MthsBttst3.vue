<template>
  <div class="MtsBase"></div>
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
  // background: #0a1122;
}
</style>

<template>
  <div>
    <Message :msg="msg" v-show="msg" />
    <div>
      <form id="burger-form" @submit="createBurger">
        <div class="input-container">
          <label for="name">Nome do cliente: </label>
          <input
            type="text"
            name="name"
            id="name"
            v-model="name"
            placeholder="Digite o seu nome"
          />
        </div>
        <div class="input-container">
          <label for="bread">Escolha o pão: </label>
          <select name="bread" id="bread" v-model="bread">
            <option value="">Selecione o seu pão</option>
            <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
              {{ pao.tipo }}
            </option>
          </select>
        </div>
        <div class="input-container">
          <label for="meat">Escolha a carne: </label>
          <select name="meat" id="meat" v-model="meat">
            <option value="">Selecione o tipo de carne</option>
            <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
              {{ carne.tipo }}
              <!-- <option value="pork">Pork</option> -->
            </option>
          </select>
        </div>
        <div id="options-container" class="input-container">
          <label for="options">Selecione os opcionais: </label>
          <div
            class="checkbox-container"
            v-for="opcional in opcionaisdata"
            :key="opcional.id"
          >
            <input
              type="checkbox"
              name="options"
              v-model="options"
              :value="opcional.tipo"
            />
            <span>{{ opcional.tipo }}</span>
          </div>
        </div>
        <div class="input-container">
          <input type="submit" value="Criar meu Burguer!" class="submit-btn" />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Message from "@/components/Message.vue";
export default {
  name: "BurgerForm",
  components: {
    Message,
  },
  data() {
    return {
      paes: null,
      carnes: null,
      opcionaisdata: null,
      name: null,
      bread: null,
      meat: null,
      options: [],
      msg: null,
    };
  },
  methods: {
    async getIngredients() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();
      this.paes = data.paes;
      this.carnes = data.carnes;
      this.opcionaisdata = data.opcionais;
    },
    async createBurger(e) {
      e.preventDefault();
      const data = {
        name: this.name,
        meat: this.meat,
        bread: this.bread,
        options: Array.from(this.options),
        status: "Solicitado",
      };
      const dataJson = JSON.stringify(data);
      const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });
      const res = await req.json();

      //set msg
      this.msg = `Pedido Nº${res.id} realizado com sucesso!`;

      //clear msg
      setTimeout(() => (this.msg = ""), 2500);

      //clear form
      this.name = "";
      this.bread = "";
      this.meat = "";
      this.options = "";
    },
  },
  mounted() {
    this.getIngredients();
  },
};
</script>

<style scoped>
#burger-form {
  max-width: 400px;
  margin: 0 auto;
}
.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}
label {
  font-weight: bold;
  margin-bottom: 15px;
  color: #222;
  padding: 5px 10px;
  border-left: 4px solid #fcba03;
}
input,
select {
  padding: 5px 10px;
  width: 300px;
}
#options-container {
  flex-direction: row;
  flex-wrap: wrap;
}

#options-title {
  width: 100%;
}
.checkbox-container {
  display: flex;
  align-items: flex-start;
  width: 50%;
  margin-bottom: 20px;
}
.checkbox-container span,
.checkbox-container input {
  width: auto;
}
.checkbox-container span {
  margin-left: 6px;
  font-weight: bold;
}
.submit-btn {
  background-color: #222;
  color: #fcba03;
  font-weight: bold;
  border: 2px solid #222;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: 0.5s;
}
.submit-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>

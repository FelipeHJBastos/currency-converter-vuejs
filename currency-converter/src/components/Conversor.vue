<template>
  <div class="conversor">
    <h2>{{ moedaA }} To {{ moedaB }}</h2>
    <input type="text" v-model="moedaA_value" v-bind:placeholder="moedaA" />
    <input type="button" value="Converter" v-on:click="convert" />
    <h2>{{ moedaB_value }}</h2>
  </div>
</template>

<script>
export default {
  name: "Conversor",
  props: ["moedaA", "moedaB"],

  data() {
    return {
      moedaA_value: "",
      moedaB_value: 0,
    };
  },
  methods: {
    async convert() {
      let from_to = this.moedaA + "_" + this.moedaB;

      let url =
        "https://free.currconv.com/api/v7/convert?q=" +
        from_to +
        "&compact=ultra&apiKey=48405bd9db2ac2d6da46";

      let response = await fetch(url);
      response = await response.json();

      console.log(response[from_to]);
      let conversion = response[from_to];
      this.moedaB_value = (conversion * parseFloat(this.moedaA_value)).toFixed(
        2
      );
    },
  },
};
</script>

<style>
.conversor {
  padding: 20px;
  max-width: 300px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
}
</style>
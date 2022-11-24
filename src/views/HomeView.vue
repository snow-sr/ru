<script>
import axios from "axios";
import TempoCidade from "@/components/TempoCidade.vue";
export default {
  data() {
    return {
      cidadeSelecionada: "",
      cidadeBuscada: null,
      bandeira: "",
    };
  },
  methods: {
    async getWheater() {
      axios
        .get(
          `http://api.weatherapi.com/v1/current.json?key= 699dc7b3708143ebac3120657222411&q=${this.cidadeSelecionada}&aqi=no`
        )
        .then((res) => {
          console.log(res.data);
          this.cidadeBuscada = res.data;
          this.bandeira = `https://countryflagsapi.com/png/${this.cidadeBuscada.location.country.toLowerCase()}`;
        });
    },
  },
  components: {
    TempoCidade,
  },
};
</script>

<template>
  <div>
    <div class="flex flex-col justify-center items-center">
      <div class="w-1/2 bg-white rounded-lg shadow-lg p-6 m-4">
        <div class="flex justify-between items-center">
          <h1 class="text-2xl font-bold">
            Insira uma cidade, e veja a previsão do tempo:
          </h1>
        </div>
        <div class="mt-8">
          <form @submit.prevent="getWheater">
            <div class="flex justify-between items-center">
              <input
                type="text"
                class="w-full border rounded-lg px-3 py-2"
                placeholder="Cidade"
                v-model="cidadeSelecionada"
              />
              <button
                type="submit"
                class="bg-blue-500 text-white px-4 py-2 rounded-lg ml-4"
              >
                Buscar
              </button>
            </div>
          </form>
        </div>
      </div>
      <div v-if="cidadeBuscada">
        <TempoCidade :cidade="cidadeBuscada" :bandeira="bandeira" />
      </div>
    </div>
  </div>
</template>

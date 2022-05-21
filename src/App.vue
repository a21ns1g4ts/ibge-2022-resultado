<template>
  <div>
    <h1>Concurso IBGE-2022</h1>
    <p>Resultado final do concurso do IBGE 2022 divulgado pela FGV</p>

    <form @submit.prevent="searchParticipant">
      <input type="text" v-model="search" placeholder="Pesquisar (nome)" />

      <button type="submit">Pesquisar</button>
    </form>

    <ul>
      <strong v-if="results.length">
        Inscrição Nome Nascimento Jurado Objetiva Final Situação Classificação
        Cidade
      </strong>
      <div v-for="(result, i) in results" :key="i">
        <p>
          {{ result.participant }} <strong>{{ result.city }}</strong>
        </p>
      </div>
    </ul>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data: function () {
    return {
      data: null,
      search: "",
      results: [],
    };
  },

  methods: {
    searchParticipant: function () {
      this.results = this.data.filter(
        function (item) {
          return (
            item.participant.toLowerCase().indexOf(this.search.toLowerCase()) >
            -1
          );
        }.bind(this)
      );
    },
  },

  mounted: function () {
    fetch("/results.json")
      .then((res) => res.json())
      .then((data) => {
        this.data = data;
      });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

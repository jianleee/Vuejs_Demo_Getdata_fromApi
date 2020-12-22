<template>
  <div id="App">
    <h1>BitCoin Index in real time</h1>

    <section v-if="errored">
      <h2>Sorry we can't update data right now :(</h2>
    </section>

    <section v-else>
      <div v-if="loading">Loading...</div>
      <div v-else v-for="data in info" :key="data.index" class="wrapper">
        <img
          src="https://cdn.vietnambiz.vn/2019/8/10/sis-dilemma-ttg-topofmind-750x350-e14951336804161-1565426422753613744677.png"
        />
        <div>
          <h2>{{ data.description }}</h2>
          <h4>Rate: {{ data.rate }} <i class="fas fa-comment"></i></h4>
          <h5>Unit: <span v-html="data.symbol"></span></h5>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      info: null,
      loading: true,
      errored: false,
    };
  },
  mounted() {
    axios
      .get("https://api.coindesk.com/v1/bpi/currentprice.json")
      .then((response) => {
        this.info = response.data.bpi;
      })
      .catch((error) => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  },
};
</script>

<style>
h1, h2{
  color: rgb(97, 74, 74)
}
#App {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin: auto;
  width: 60%;
  background-color: rgb(236, 230, 230);
  border-radius: 3px;
  padding: 10px;
}
.wrapper {
  display: flex;
  margin-bottom: 10px;
  border-bottom: 2px solid black;
}
img {
  width: 300px;
  height: 200px;
  display: block;
  margin-right: 5px;
}
</style>

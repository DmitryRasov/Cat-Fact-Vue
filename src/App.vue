<template>
  <div class="container">
    <div class="fact-wrapper">
        {{ info }}
    </div>
    <div class="button">
      <button class="btn" @click="getFact">{{ this.factIsLoading === true ? 'Loading...' : btnTitle }}</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";


export default {
  components: {},
  data() {
    return {
      btnTitle: 'Start',
      info: 'Here will be the fact',
      zeroIndex: 0,
      factIsLoading: false
    }
  },
  methods: {
    async getFact() {
  const randomFact = Math.round(Math.random() * 330)
      this.factIsLoading = true
  await
      axios
          .get('https://catfact.ninja/facts?max_length=1000&limit=1000')
          .then(response => {
            this.info = response.data.data[randomFact].fact
            console.log(this.info)
          })
          .catch(error => alert(error))
          this.factIsLoading = false;
          this.btnTitle = 'Another one'
    },
  }
}


</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans&display=swap');
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
html {
  height: 100vh;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: bold;
}
body {
  background: url("assets/23448490.jpg");
  display: flex;
  align-items: center;
  justify-content: center;

  height: 100%;
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;

  max-width: 500px;
  margin: 15px;
  border: 1px solid deeppink;
  border-radius: 5px;
  background: #BC8FD9E8;
}
.fact-wrapper {
  padding: 15px;
  font-size: 30px;
  min-height: 100px;
}
.button {
  padding: 0 15px 15px 15px;
}
.btn {
  padding: 7px 20px;
  border: 1px solid deeppink;
  border-radius: 5px;
  /*border: none;*/
  cursor: pointer;
  -webkit-appearance: none;
}
.btn:hover {
  box-shadow: 4px 4px 8px 0 rgba(251, 103, 253, 0.2);
  transition: .3s;
}
@media screen and (max-width: 424px) {
.fact-wrapper{
  font-size: 20px;
  min-height: auto;
  }
}
</style>
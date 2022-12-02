<template>
  <div>
    <h1>Hello 👋, Welcome to our travel suggest app</h1>
    <p>Select a continent and we will suggest awesome locations for you to visit</p>
    <div>
      <select v-model="continent" class="select" @change="getCountry">
        <option value="" selected disabled>Select a Continent</option>
        <option value="Asia">Asia</option>
        <option value="Africa">Africa</option>
      </select>
      <span><img src="../assets/refresh.png" @click="getCountry" class="refresh_image" alt=""></span>
    </div>
    <div v-if="show_suggestion">
      <hr>
      <h1>Viola!, we suggest you travel to <i class="suggested_county">{{ suggested_country }}</i></h1>
      <h1>Bon Voyage ✈️ </h1>
    </div>
  </div>
</template>

<script>
import axios from "axios"

export default {
  name: 'Suggest',
  data() {
    return {
      backend_url: process.env.VUE_APP_BACKEND_URL,
      continent: "",
      suggested_country: "",
      show_suggestion: false
    }
  },
  methods: {
    getCountry() {
      if (this.continent === "") {
        alert("no country selected")
      }
      else {
        axios.get(this.backend_url + `suggest?continent=${this.continent}`).then(resp => {
          this.suggested_country = resp.data["country"]
          this.show_suggestion = true
        });
      }

    }
  },
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.select {
  font-size: 2rem;
  width: 25rem;
  vertical-align: middle;
  padding: 0.3rem;
}

.refresh_image {
  height: 4rem;
  vertical-align: middle;
  cursor: pointer;
}
.refresh_image:hover {
  height: 3.8rem;
}

.suggested_county {
  color: #168f21;
  font-size: 5rem;
  font-weight: bold
}
</style>

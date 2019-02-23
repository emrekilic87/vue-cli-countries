<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div class="selectArea">
    <select name="select" id="select" v-model="selected" :required="true" @change="selectContry()">
      <option value="Choose Country" >Choose Country</option>
      <option value="All" >All Country</option>
      <option v-for="item in results" v-bind:value="item.alpha3Code" >{{item.name}}</option>
    </select>
    </div>
    <div id="result">
      <div class="container">
        <div class="row justify-content-center">
          <div class="resultArea col-12 col-md-4" v-for="item in results" v-if="selected == item.alpha3Code">
            <div class="name">
              <strong>Country Name: </strong>
              <span>{{item.name}}</span>
            </div>
              <div class="nativeName">
              <strong>Native Name: </strong>
              <span>{{item.nativeName}}</span>
            </div>
            <div class="capital">
              <strong>Capital: </strong>
              <span>{{item.capital}}</span>
            </div>
            <div class="flag">
              <img v-bind:src="item.flag" alt>
            </div>
          </div>

             <div class="resultArea col-12 col-md-4" v-for="item in results" v-if="selected == 'All'">
            <div class="name">
              <strong>Country Name: </strong>
              <span>{{item.name}}</span>
            </div>
              <div class="nativeName">
              <strong>Native Name: </strong>
              <span>{{item.nativeName}}</span>
            </div>
            <div class="capital">
              <strong>Capital: </strong>
              <span>{{item.capital}}</span>
            </div>
            <div class="flag">
              <img v-bind:src="item.flag" alt>
            </div>
          </div>

          <div class="any resultArea col-12 col-md-4" v-if="selected == 'Choose Country'">
            Any Country Selected!!
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue';
import axios from "axios";

export default {
  name: "home",
  components: {
    // HelloWorld,
  },
  data() {
    return {
      results: null,
      selected: "All"
    };
  },
  created() {
    axios.get("https://restcountries.eu/rest/v2/all").then(response => {
      this.results = response.data;
      console.log(response.data);
    });
  },
  method:{
     selectContry() {
    
    }
  }
};
</script>

<style scoped>
img{
  width:100%;
}

.selectArea{
  width:320px;
  margin: 0 auto 2em
}

.selectArea select{
  width:100%;
}

.resultArea{
  margin-bottom: 2em
}

.any.resultArea{
  font-size: 20px;
}
</style>


<template>
<div>
<div v-if='error === true' class="container">
  Oh snap, something has gone wrong:
  <br/>
  {{errorMessage}}
</div>
 <nav-bar @addBeer="addBeer"></nav-bar>
 <cooler @deleted='deleteBeer' @upvoted="upvoted" @downvoted="downvoted" :beers='this.beers'></cooler>
 </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
Vue.use(VueAxios, axios);
var _ = require('lodash/core');

export default {
  name: 'app',
  data:function(){
    return {
      error:false,
      errorMessage:"",
      beers: {}
    }
  },
  components: {
    'nav-bar':require('./components/nav.vue'),
    'cooler':require('./components/cooler.vue'),

  },
  created:function(){
    this.getBeers();
  },
  methods:{
    getBeers:function(){

      //unfortuntely have to do this because of axios
      let self = this;

      Vue.axios.get('api/beer/')
        .then(function (response) {
        self.beers = response.data;
      })
      .catch(function (error) {
        self.error = true;
        self.errorMessage = error;
      });
    },
    getSingleBeer:function(id){

      let self = this;

      Vue.axios.get('api/beer/'+id)
        .then(function (response) {

      })
      .catch(function (error) {

      });
    },
    addBeer:function(newBeer){

      let self = this;

      self.getBeers();

      let lookForName = _.filter(this.beers, function(b){
        return b.name === newBeer.name;
      });

      if(lookForName.length < 1){
        Vue.axios.post('api/beer', {
          name: newBeer.name,
          likes: newBeer.likes
        })
        .then(function (response) {
          self.getBeers();
        })
        .catch(function (error) {
          self.error = true;
          self.errorMessage = error;
        });
      }else{
        self.error = true;
          self.errorMessage = 'Whoops, that beer was already listed.';
      }
    },
    updateBeer:function(beer){

      let self = this;

      Vue.axios.put('api/beer/'+beer.id, {
        likes: beer.likes
      })
      .then(function (response) {
      })
      .catch(function (error) {
        self.error = true;
        self.errorMessage = error;
      });
    },

    deleteBeer:function(id){

      let self = this;

      Vue.axios.delete('api/beer/'+id)
      .then(function (response) {
          self.getBeers();
      })
      .catch(function (error) {
        self.error = true;
        self.errorMessage = error;
      });
    },


    upvoted:function(id){
      var self = this;
      self.beers.forEach(function(beer){
        if(beer.id === id){
          beer.likes = beer.likes + 1;
          self.updateBeer(beer);
        }
      })
    },
    downvoted:function(id){
       var self = this;
      this.beers.forEach(function(beer){
        if(beer.id === id){
          beer.likes = beer.likes - 1;
          self.updateBeer(beer);
        }
      })
    },
    deleted:function(id){

    }
  }
}

</script>

<style>

</style>

<template>
 <div class="container">
 <div class="justify-content-center my-1">
  <b-table striped :items="beerArray" :fields="fields">
    <template slot="id" scope="item">
      <voting-buttons @delete='deleted' @downvote='downvoted' @upvote='upvoted' :id='item.value'></voting-buttons>
    </template>
    <template slot="name" scope="item">
     {{item.value}}
    </template>
    <template slot="likes" scope="item">
       {{item.value}}
    </template>
  </b-table>
</div>
 </div>
</template>

<script>


export default {
  name: 'cooler',
  props: ['beers'],
  data:function(){
    return {
      fields:{
        id:{
          label:"",
          sortable:false
        },
        name:{
          label:"Beer Name",
          sortable:true
        },
        likes:{
          label:"Likes",
          sortable:true
        }
      }
    }
  },
  components: {
    'voting-buttons':require('./votingButtons.vue')
  },
  created:function(){
    this.beerList = this.beers;
  },
  computed:{
    beerArray:function(){
      return Array.prototype.slice.call(this.beers, 0);
    }
  },
  methods:{
    upvoted:function(id){
      this.$emit('upvoted',id);
    },
    downvoted:function(id){
      this.$emit('downvoted',id);
    },
    deleted:function(id){
      this.$emit('deleted',id);
    }
  }
}

</script>

<style>
.table th, .table td {
    padding: 0.5rem;
    vertical-align: baseline;
}
</style>
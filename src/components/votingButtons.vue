<template>
 <div>
  <b-button-group vertical>
    <b-button v-on:click='upvote'><i class="fa fa-thumbs-up" aria-hidden="true"></i></b-button>
    <b-button v-on:click='deleted' variant="danger">Remove</b-button>
    <b-button v-on:click='downvote'><i class="fa fa-thumbs-down" aria-hidden="true"></i></b-button>
  </b-button-group>
 </div>
</template>

<script>


export default {
  name: 'voting-buttons',
  props:['id'],
  data:function(){
    return {

    }
  },
  components: {

  },
  created:function(){

  },
  methods:{
    upvote:function(){
      this.$emit('upvote', this.id);
    },
    downvote:function(){
      this.$emit('downvote', this.id);
    },
    deleted:function(id){
      this.$emit('delete', this.id);
    }
  }
}

</script>

<style>

</style>
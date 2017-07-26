<template>
  <b-navbar toggleable type="inverse" variant="success">

    <b-nav-toggle target="nav_collapse"></b-nav-toggle>

    <b-link class="navbar-brand" to="#">
      <span>FluentStream Cooler</span>
    </b-link>

    <b-collapse is-nav id="nav_collapse">


      <b-nav is-nav-bar class="ml-auto">

        <!-- Navbar dropdowns -->
        <b-nav-item right v-b-modal.modal1 >Add A Beer</b-nav-item>

      </b-nav>
    </b-collapse>

    <b-modal id="modal1" title="Add A Beer" @ok="submit" @shown="clearName">
    <div> Please click ok, don't hit enter.  I mean you can if you want to actually but the modal won't autoclose</div>
    <form @submit.stop.prevent="submit">
      <b-form-input type="text" placeholder="Enter a beer." v-model="newBeer.name"></b-form-input>
    </form>

  </b-modal>
  </b-navbar>

</template>

<script>


export default {
  name: 'nav-bar',
  data:function(){
    return {
      newBeer:{
        name:'',
        likes:0
      }
    }
  },
  components: {
    'add-beer':require('./addBeer.vue')
  },
  methods:{
    clearName:function(){
      this.newBeer.name = "";
    },
    submit:function(event){
       if (!this.newBeer.name) {
          alert('Please enter a beer.');
        }else{
          this.$emit('addBeer', this.newBeer);
        }
    }
  }
}
</script>

<style>

</style>

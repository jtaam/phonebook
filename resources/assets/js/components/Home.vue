<template>
  <div>
    <nav class="panel column is-offset-2 is-8">
      <p class="panel-heading">
        VueJs Phonebook
        <button @click="openAdd" class="button is-link is-outlined">
          Add New
        </button>
        <span class="is-pulled-right" v-if="loading">
          <i class="fa fa-refresh fa-spin fa-2x fa-fw"></i>
        </span>
      </p>
      <div class="panel-block">
        <p class="control has-icons-left">
          <input class="input is-small" type="text" placeholder="search">
          <span class="icon is-small is-left">
            <i class="fas fa-search" aria-hidden="true"></i>
          </span>
        </p>
      </div>


      <a class="panel-block" v-for="item,key in lists">
        <span class="column is-9">
          {{item.name}}
        </span>
        <span class="panel-icon column is-1">
          <i @click="delItem(key, item.id)" class="has-text-danger fa fa-trash" aria-hidden="true"></i>
        </span>
        <span class="panel-icon column is-1">
          <i @click="openUpdate(key)" class="has-text-info fa fa-edit" aria-hidden="true"></i>
        </span>
        <span class="panel-icon column is-1">
          <i @click="openShow(key)" class="has-text-primary fa fa-eye" aria-hidden="true"></i>
        </span>
      </a>
    </nav>
    <Add :openmodal='addActive' @closeRequest='close'></Add>
    <Show :openmodal='showActive' @closeRequest='close'></Show>
    <Update :openmodal='updateActive' @closeRequest='close'></Update>
  </div>
</template>

<script>
let Add = require('./Add.vue');
let Show = require('./Show.vue');
let Update = require('./Update.vue');
  export default{
    components:{Add,Show,Update},
    data(){
      return {
        addActive: '',
        showActive: '',
        updateActive: '',
        lists:{},
        errors:{},
        loading:false
      };
    },
    mounted(){
      axios.post('/getData')
        .then((response)=> this.lists = response.data)
        .catch((error) => this.errors = error.response.data.errors)
    },// mounted
    methods:{
      openAdd(){
        this.addActive = 'is-active'
      },
      openShow(key){
        this.$children[1].list = this.lists[key]
        this.showActive = 'is-active'
      },
      openUpdate(key){
        this.$children[2].list = this.lists[key]
        this.updateActive = 'is-active'
      },
      close(){
        this.addActive = this.showActive = this.updateActive = ''
      },
      delItem(key, id){
        if (confirm("Are you sure ?")) {
					this.loading = !this.loading
					axios.delete(`/phonebook/${id}`)
					.then((response)=> {this.lists.splice(key,1);this.loading = !this.loading})
					.catch((error) => this.errors = error.response.data.errors)
				}
				console.log(`${key} ${id}`)
      }
    }
  }
</script>

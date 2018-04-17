<template>
  <div class="modal" :class='openmodal'>
    <div class="modal-background"></div>
    <div class="modal-card">
      <header class="modal-card-head">
        <p class="modal-card-title">Modal title</p>
        <button @click='close' class="delete" aria-label="close"></button>
      </header>
      <section class="modal-card-body">
        <div class="field">
          <label class="label">Name</label>
          <div class="control">
            <input :class="{'is-danger':errors.name}" v-model="list.name" class="input is-primary" type="text" placeholder="Name">
          </div>
          <small v-if="errors.name" class="has-text-danger">{{errors.name[0]}}</small>
        </div>
        <div class="field">
          <label class="label">Phone</label>
          <div class="control">
            <input :class="{'is-danger':errors.phone}" v-model="list.phone" class="input is-primary" type="number" placeholder="Phone">
            <small v-if="errors.phone" class="has-text-danger">{{errors.phone[0]}}</small>
          </div>
        </div>
        <div class="field">
          <label class="label">Email</label>
          <div class="control">
            <input :class="{'is-danger':errors.email}" v-model="list.email" class="input is-primary" type="email" placeholder="Email">
            <small v-if="errors.email" class="has-text-danger">{{errors.email[0]}}</small>
          </div>
        </div>
      </section>
      <footer class="modal-card-foot">
        <button @click='save' class="button is-success">Save changes</button>
        <button @click='close' class="button">Cancel</button>
      </footer>
    </div>
  </div>
</template>

<script>
  export default{
    props:['openmodal'],
    data(){
      return {
        list:{
          name:'',
          phone:'',
          email:''
        },
        errors:{}
      } // return
    }, // data
    methods:{
      close(){
        this.$emit('closeRequest')
      },
      save(){
        axios.post('/phonebook', this.$data.list).then((response)=> this.close())
          .catch((error) => this.errors = error.response.data.errors)
      } // save
    } // methods
  }
</script>

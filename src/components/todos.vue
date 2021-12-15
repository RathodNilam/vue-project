<template>
	<div>
		<transition name="todos">
        

  <b-modal id="modal-1" title="Now To Do">
    <b-form v-on:submit.prevent="submit">
  
      <div class="row">
        <div class="col-12">
          <label>Name</label>
        </div>
        <div class="col-12">
          <input type="text" class="form-control" v-model="form.name"/>
          <br>
        </div>
        <div class="col-12">
        <label>Text</label>
        </div>
        <div class="col-12">
          <input type="text" class="form-control" v-model="form.text"/>
            <br>
        </div>
        <button class="btn btn-primary">submit</button>
      </div>
    </b-form>
    </b-modal>
      </transition>
	</div>
</template>
<script>
import axios from "axios";
export default{
  data:function(){
    return{
      form:{
      name:'',
      text:''
      } 
    };
  },

  methods:{
    submit:function(){
        return axios
      .post("http://localhost:8000/api/AddTodos",this.form)
      .then(response=>{
        console.log(response);
       
      }).catch(err => {
        alert(err);
      }); 
    }
  }
}
</script>
  
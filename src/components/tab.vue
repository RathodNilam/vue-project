S<template>
    <div>
        <div class="container-fluid">
            <div class="row">
            <div class="col-12">
            <div class="logo">
            <h5><strong>Logo</strong></h5>
            </div>
            </div>
            </div>

            <br>
            <div class="container">
            <div class="tab">
            <ul class="nav nav-tabs">
                <li class="nav-item">
                    <a class="nav-link" @click.prevent="setActive('todos')" :class="{active:isActive('todos')}" href="#todos">Todos</a>
                </li>

                <li class="nav-item">
                    <a class="nav-link" @click.prevent="setActive('post')" :class="{active:isActive('post')}" href="#post">Post</a>
                </li>

                <li class="nav-item">
                    <a class="nav-link" @click.prevent="setActive('myInfo')" :class="{active:isActive('myInfo')}" href="#myInfo">My Info</a>
                </li>
            </ul>
        </div>

            <div class="tab-content">
                <div class="tab-pane fade" :class="{'active show':isActive('todos')}" id="todos">

                    <br>
                    <div class="row">
                        <div class="col-4">
                            <input type="text" placeholder="Search" v-model="searchQuery" />
                        </div>

                        <div class="col-8">
                            <!-- <button class="btn btn-addnew" id="open-modal" @click="openModal=true">Add New</button> -->
                            <b-button v-b-modal.modal-1 id="open-modal">Add New</b-button>
                        </div>

                    </div>
                            <todos v-if="openModal" @close="openModal=false">
                            </todos>
                            <br>
                        <table class="table">
                            <thead>
                                <th>Todo</th>
                                <th>Text</th>
                                <th>Action</th>
                            </thead>
                            <tbody>
                                <tr v-for="(todo,index) in resultQuery" :key="index">
                                    <td>{{todo.name}}</td>
                                    <td>{{todo.text}}</td>
                                    <td><a @click="removeTodoRow(index)"><b-icon icon="trash"></b-icon></a></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>

                <div class="tab-pane fade" :class="{'active show':isActive('post')}" id="post">
                    <br>
                    <div class="row">

                        <div class="col-4">
                            <input type="text" placeholder="Search"  v-model="searchQuery1"  />
                        </div>

                        <div class="col-8">
                            <button class="btn btn-addnew" id="open-modal" @click="openModal=true">Add New</button>
                        </div>

                    </div>
                            <post v-if="openModal" @close="openModal=false">
                            </post>

                            <br>
                            <table class="table">
                            <thead>
                                <th>Name</th>
                                <th>Text</th>
                                <th>Email</th>
                                <th>Actions</th>
                            </thead>
                            <tbody>
                                <tr v-for="(post, index) in resultQuery1" :key="index">
                                    <td>{{post.name}}</td>
                                    <td>{{post.text}}</td>
                                    <td>{{post.email}}</td>
                                    <td><a @click="removePostRow(index)"><b-icon icon="trash"></b-icon></a></td>
                                </tr>
                            </tbody>
                            </table>
                </div>

                <!-- <div class="tab-pane fade" :class="{'active show':isActive('myInfo')}" id="myInfo">
                    <user-info></user-info>
                </div> -->

            </div>
        </div>
    </div>
</div>


</template>
 
<script>
    import axios from "axios";

    export default {
    data:function() {
        return{
             activeItem: 'todos',
             openModal:false,
             searchQuery: null,
             searchQuery1: null,
             todos: [],
    posts: [
    {name: "PHP",text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit",email:"abc@gmail.com"},
      {name: "Flutter",text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit",email:"abc@gmail.com"},
      {name: "IOS",text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit",email:"abc@gmail.com"},
      {name: "Android",text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit",email:"abc@gmail.com"},
      {name: "Laravel",text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit",email:"abc@gmail.com"},
      {name: "ReactJs",text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit",email:"abc@gmail.com"},
      {name: "Vuejs",text: "Lorem ipsum dolor sit amet, consectetur adipiscing elit",email:"abc@gmail.com"},
    ]

        }; 
    },

    computed: {
    resultQuery(){
      if(this.searchQuery){
      return this.todos.filter((todo)=>{
        return this.searchQuery.toLowerCase().split(' ').every(v => todo.name.toLowerCase().includes(v))
      })
      }else{
        return this.todos;
      }
    },
    resultQuery1(){
      if(this.searchQuery1){
      return this.posts.filter((post)=>{
        return this.searchQuery1.toLowerCase().split(' ').every(v => post.name.toLowerCase().includes(v))
      })
      }else{
        return this.posts;
      }
    }
  },

  created()
  {

        return axios.get("http://localhost:8000/api/GetTodos")
      .then(response=>{
        console.log(response);
    this.todos = response.data;
      }).catch(err => {
        alert(err);
      }); 
    },




    methods: {
    isActive (menuItem) {
      return this.activeItem === menuItem
    },

    setActive (menuItem) {
      this.activeItem = menuItem
    },

    removeTodoRow: function (index) {
    console.log(index);
    this.todos.splice(index,1);
    },

    removePostRow: function (index) {
    console.log(index);
    this.posts.splice(index,1);
    }

    }
    }
</script>

<style>
    body{
        overflow-x: hidden;
        background-color: #fff;
    }
    .container-fluid{
        padding-left: 0px;
        padding-right: 0px;
    }
    .container{
        width: 68% !important;
    }
    .logo{
        padding:8px 0px 1px 25px;
        background-color: lightgrey;
    }
    .nav-tabs .nav-link.active{
        background-color: #dee2e6;
        font-weight: 600;
    }
    .tab{
        margin-top: 70px;
        /*margin-left: 245px;*/
    }
    .nav-tabs{
        border-bottom: 0px;
    }
    a{
        color: black;
    }
    a:hover{
        color: black;
    }
    .nav-link{
        padding:0.5rem 4rem;
        
    }
    .nav-tabs .nav-link{
        border-top-left-radius: inherit;
        border-top-right-radius: inherit;
    }
    input{
        width: 100%;
    }
    input[placeholder="Search"]{
        padding-left: 10px;
        font-weight: 600;
    }
    .btn-addnew{
       background-color: lightgray;
       float: right;
       border-radius: 0px;
       font-weight: 600;
    }
    .table td{
        border-top: 0px;
    }
    .table thead th{
        border-top:0px;
        border-color:black;
        border-width: thin;
    }
</style>
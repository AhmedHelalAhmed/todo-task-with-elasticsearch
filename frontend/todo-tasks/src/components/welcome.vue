<template>
  <div>



    <div class="container text-center notAuth">

      <div class="row">


        <div class="col-lg-12">
          <div class="media">
            <a class="pull-left" href="#">

              <img class="media-object dp img-circle" src="http://img.app-liv.jp.s3.amazonaws.com/icon/003090831/26a250e865c6d36819efbe6badcee2f1.png" style="width: 100px;height:100px;">

            </a>
            <div class="media-body">



              <h3 class="media-heading">Welcome in <span>TODO</span></h3>



              <hr style="margin:8px auto">

              <h4>Please <small><router-link  :to="{path: '/login'}" class="py-2 d-none d-md-inline-block">Login</router-link></small> or <small><router-link v-if="!this.$auth.isAuth()" :to="{path: '/register'}" class="py-2 d-none d-md-inline-block">Register</router-link></small></h4>

            </div>
          </div>

        </div>



      </div>
    </div>

    <div v-if="this.$auth.isAuth()" class="container text-center">
      <addtasks
        v-if="app_key&&app_create_key&&!route_name"
        v-on:addTask="listenToAddTask($event)">
      </addtasks>

      <showtasks
        v-if="app_key&&app_create_key&&!route_name"
        v-bind:newTask="tasks"
        v-on:changeView="listenToChangeView($event)">
      </showtasks>



      <div
        v-on:click="callCreateTask()"
        v-if="app_create_key&&app_key&&!route_name">
        <router-link
          :to="{path: '/create'}"
          class="btn btn-success">
          Create a Task
        </router-link>
      </div>

    </div>


  </div>
</template>
<script>
import AddTasks from './addtasks.vue'
import ShowTasks from './showtasks.vue'
import CreateTask from './createtask.vue'
import ShowTask from './showtask.vue'
import EditTask from './edittask.vue'
import Login from './login.vue'
import Header from './header.vue'
import Footer from './footer.vue'

// import {bus} from './main';


export default {
  components: {
    'addtasks': AddTasks,
    'showtasks': ShowTasks,
    'createtask': CreateTask,
    'login': Login,
    'app-header': Header,
    'app-footer': Footer,
  },


  data() {
    return {
      //just contain new data
      tasks: [], //for new task that will be added
      title: 'todo', //title of the app
      description: '', //for add new task
      app_key: true, //flag for show tasks and add tasks components and app
      app_create_key: true, //flag for create task component and the rest of components
      route_name: this.$route.name,
    }
  },

  methods: {
    listenToAddTask(e) {
      //e = the value entered by user
      this.tasks.push(e);
    },
    listenToChangeView(e) {
      this.app_key = e;
      this.route_name = null;
    },
    callCreateTask() {
      this.app_create_key = false;
      this.route_name = null;
    },
    listenToCreateTask(e) {
      this.app_create_key = e;
      this.route_name = null;
    }

  },
  created() {

  },
  mounted(){



    // bus.$emit('send_data',[this.app_key,this.app_create_key]);


  }

}
</script>

<style scoped>



  div .notAuth{
    margin-top: 30%;
    display: flex;
    justify-content: center;
  }

  .media-heading span{
    color: red;
    font-weight: bold;
  }


  h1 {
    color: purple
  }

  a{
    color: #001b44;
  }

</style>

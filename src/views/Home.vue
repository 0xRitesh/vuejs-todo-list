<template>
  <div id="app">
    <Form v-on:addTodo='addTodo' />
    <Todos v-bind:Todos='Todos' v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>

import Form from '../components/form'
import Todos from '../components/todos'
import axios from 'axios'
import swal from 'sweetalert';

export default {
  name: "Home",
  components: {
    Form,
    Todos
  },

  data() {
    return {
      Todos: [
        {
          uniqueId: 1,
          title: 'meeting at 9',
          completed: false,
          id: 1
        },
        {
          uniqueId: 2,
          title: 'review your monthly Budget',
          completed: false,
          id: 2
        },
        {
          uniqueId: 3,
          title: 'update windows ',
          completed: false,
          id: 3
        },
        {
          uniqueId: 4,
          title: 'meeting at 9',
          completed: false,
          id: 4
        },
        {
          uniqueId: 5,
          title: 'review your monthly Budget',
          completed: false,
          id: 5
        },
        {
          uniqueId: 6,
          title: 'update windows ',
          completed: false,
          id: 6
        }
      ],
    }
  },

  methods: {
    deleteTodo(uniqueId) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${uniqueId}`)
      .then(res => {

        swal({
          title: "Are you sure?",
          text: "You will not be able to recover this todo!",
          icon: "warning",
          buttons: true,
          dangerMode: true,
          trash: res
        })
        .then((willDelete) => {
          if (willDelete) {
            swal(`Poof! Todo deleted!`, {
              icon: "success",
            });
            this.Todos = this.Todos.filter(todo => todo.uniqueId !== uniqueId);
          } else {
            swal("Your todo is safe");
          }
        });
      })
      .catch(err => console.log(err))
    },

    addTodo(todo) {
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        uniqueId: this.Todos.length + 1,
        title: todo,
        completed: false
      })
      .then(res => this.Todos = [...this.Todos, res.data])
      .catch(err => console.log(err))
      // this.Todos.push ({
      //   id: this.Todos.length + 1,
      //   title: todo,
      //   completed: false
      // })
    },
  },

  // created() {
  //   axios.get('https://jsonplaceholder.typicode.com/todos?_limit=1')
  //   .then(res => {this.Todos = res.data + this.Todos})
  //   .catch(err => console.log(err))
  // }

};
</script>

<style>
 * {
    margin: 0;
    padding: 0;
    --primary-color: #42b983;
    font-family: Avenir, Helvetica, Arial, sans-serif;
  }
</style>

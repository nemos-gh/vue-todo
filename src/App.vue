<template lang="pug">
  #app 
    ActionBar(@addNew="togglePanel")
    h1 Todo List
    TodoList(:todos="todos" @remove-todo="removeTodo")
    transition(name="slide")
      NewTodo(
        v-if="showAddNew" 
        @hidePanel="togglePanel" 
        @addTodo="addTodo")
    footer 
      p nb &copy; 2018 | Playin' around with the 
        a(href="https://vuejs.org/" target="_blank") Vue
        |  framework.
</template>

<script>
import ActionBar from './components/ActionBar'
import TodoList from './components/TodoList'
import NewTodo from './components/NewTodo'

export default {
  name: 'app',
  components: {
    ActionBar,
    TodoList,
    NewTodo
  },
  data() {
    return {
      todos: [
        {id: '0', text: 'Learn Vue, it\'s great!'},
        {id: '1', text: 'Learn Vue! 👍'},
        {id: '3', text: 'Learn Vue, it\'s great!'},
        {id: '4', text: 'Learn Vue, Learn Vue 🙇😀🖖'},
        {id: '6', text: 'Vuuueeeee... 🤪😎'},
      ],
      showAddNew: false
    }
  },
  methods: {
    togglePanel() {
      this.showAddNew = ! this.showAddNew
    },
    addTodo(el) {
      let theNew = {};
      theNew['id'] = this.uniqueId();
      theNew['text'] = el.target.value;

      if(theNew.text.trim() != '') this.todos.push(theNew);
    },
    removeTodo(id) {
      let index = this.todos.findIndex(el => el.id == id);
      this.todos.splice(index, 1);
    },
    uniqueId() {
      let rand = 0;
      do {
        rand = Math.floor(Math.random() * 10000);
      } while (this.todos.find(el => el.id == rand));
      
      return rand;
    }
  }
}
</script>

<style lang="scss">
@import './scss/reset';
@import './scss/vars';

body {
  background-color: $clr-bg;
}

h1 {
  margin-bottom: 20px;
  color: rgba($black, .2);
  font-size: 22px;
  font-family: $font-main;
  font-weight: 500;
  text-align: center;
  text-transform: uppercase;
  letter-spacing: 1px;
  word-spacing: 2px;
}

footer {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 120px;

  p {
    color: rgba($black, .5);
    font-size: 14px;
    font-family: $font-main;
  }
}

a {
  color: $black;

  &:hover {
    color: black;
    text-decoration: none;
  }
}

#app {
  margin: 0 auto 100px;
  width: 800px;
}

.slide-enter {
    margin-top: -200px;
    opacity: 0;
}

.slide-enter-active {
    transition: opacity .2s ease-in-out, margin .4s ease-in-out;
}
</style>

<template>
  <div>
    <b-container class="bv-example-row">
      <b-row>
        <b-col>
          <b-form-input v-model="newTodo" @keypress="setCanMessageSubmit" @keyup.enter="addTodo"></b-form-input>
          <div class="unDoneTodos draggable">
            <draggable
              v-model="todos"
              class="list-group"
              tag="ul"
              v-bind="dragOptions"
              @start="drag=true"
              @end="drag=false"
            >
                  <li
                    class="list-group-item"
                    v-for="(element, index) in unDoneTodos"
                    :key="index"
                  >
                    <b-form-checkbox v-model="element.isChecked"></b-form-checkbox>
                    {{ element.content }}
                  </li>
            </draggable>
          </div>
        </b-col>
        <b-col>
          <div>
            <b-button variant="success" @click="submit()">Submit</b-button>
            <b-button variant="outline-danger" @click="reset()">reset</b-button>
          </div>
        </b-col>
        <b-col>
          <div class="doneTodos">
                  <li
                    class="list-group-item"
                    v-for="(element, index) in doneTodos"
                    :key="index"
                  >
                    {{ element.content }}
                  </li>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: "home",
  components: {
    draggable
  },
  methods: {
    setCanMessageSubmit() {
      this.canMessageSubmit = true
    },
    addTodo(){
      if (!this.canMessageSubmit) {
        return
      }
      
      this.todos.unshift({
          id: 1,
          content: this.newTodo,
          isChecked: false,
          isDone: false,
      })
      this.newTodo = ""
      this.canMessageSubmit = false

    },
    submit(){
      this.todos.forEach(todo => {
          if (todo.isChecked) {
            todo.isDone = true
          }
        });
    },
    reset(){
      this.todos = [
        {
          id: 1,
          content: "todo1",
          isChecked: false,
          isDone: false,
        },
        {
          id: 2,
          content: "todo2",
          isChecked: false,
          isDone: false,
        },
        {
          id: 3,
          content: "todo3",
          isChecked: false,
          isDone: false,
        }
      ]
    }
  },
  data: function() {
    return {
      drag: false,
      checkedIDs: [],
      newTodo: "",
      canMessageSubmit: false,
      todos: [
        {
          id: 1,
          content: "todo1",
          isChecked: false,
          isDone: false,
        },
        {
          id: 2,
          content: "todo2",
          isChecked: false,
          isDone: false,
        },
        {
          id: 3,
          content: "todo3",
          isChecked: false,
          isDone: false,
        }
      ]
    };
  },
  computed: {
    unDoneTodos() {
      return this.todos.filter(function(todo){
        return (!todo.isDone)
      })
    },
    doneTodos() {
      return this.todos.filter(function(todo){
        return (todo.isDone)
      })
    },
    dragOptions() {
      return {
        animation: 200,
        group: "description",
        disabled: false,
        ghostClass: "ghost"
      };
    }
  }
};
</script>
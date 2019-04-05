<template>
  <div class="playground">
    <h1>This is an playground page</h1>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <Todo v-model="todos[index]"/>
      </li>
    </ul>
  </div>
</template>

<script>
// @ is an alias to /src
import Todo from "@/components/Todo.vue";

export default {
  name: "home",
  components: {
    Todo,
  },
  data: function() {
    return {
      todos: [
        {
          id:"1",
          content: "todo1",
          isDone: false,
          isEditing: false,
          htmlId: "todo1"
        },
        {
          id:"2",
          content: "todo2",
          isDone: false,
          isEditing: false,
          htmlId: "todo2"
        },
        {
          id:"3",
          content: "todo3",
          isDone: false,
          isEditing: false,
          htmlId: "todo3"
        }
      ]
    };
  }
};
</script>
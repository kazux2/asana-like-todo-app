<template>
  <div class="todo">
    <div v-if="!todo.isEditing" v-text="todo.content" @click="todo.isEditing = true; forceFocus()"></div>
    <input ref="todo" v-show="todo.isEditing" type="text" v-model="todo.content" @blur="todo.isEditing = false">
  </div>
</template>

<script>
export default {
  name: 'Todo',
  model: {
    prop: 'todo', //親からもらったデータの呼び名をvalueからtodoに変更
    event: 'input'
  },
  props: {
    todo: Object //親からもらったtodoオブジェクト    
  },
	methods: {
		forceFocus: function() {
      this.$nextTick(() => this.$refs.todo.focus())
		}
	}
}
</script>

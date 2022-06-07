<template>
  <div>
    <div class="new-item">
      <new-todo-form @submit="data => $emit('create', data)"/>
      <ul>
        <todo-item
          v-for="todo in list"
          :key="todo.id"
          @toggle="id => $emit('toggle', id)"
          @remove="id => $emit('remove', id)"
          :tarefa="todo"
        />
      </ul>
    </div>
  </div>
</template>
<script>
import NewTodoForm from "@/components/NewTodoForm";
import TodoItem from "@/components/TodoItem";

export default {
  components: { NewTodoForm, TodoItem },
  props: {
    list: {
      type: Array,
      default: () => []
    }
  }
};
</script>

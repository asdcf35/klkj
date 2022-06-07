<template>
  <li
    class="flex row items-center justify-between w-full py-1 px-4 my-1 rounded border bg-gray-100 text-gray-600"
  >
    <div class="items-center column">
      <input
        class="mx-1"
        type="checkbox"
        :checked="tarefa.feita === true"
        @input="$emit('toggle', tarefa.id)"
      >
      <span :class="{'line-through': tarefa.feita === true}">{{ tarefa.text }}</span>
    </div>
    <div class="items-center row-reverse">
      <span class="px-4 py-2 float-right" @click="$emit('remove', tarefa.id)">
        <i class="fas fa-times"/>
      </span>
    </div>
  </li>
</template>
<script>
export default {
  props: {
    tarefa: { type: Object, required: true }
  }
};
</script>

<template>
  <div class="new-todo-form flex column">
    <tailwind-input type="text" v-model="tarefa" placeholder="Nova tarefa" @submit="submitTarefa"/>
    <elevated-button class="ml-1" type="button" @click="submitTarefa">
      <i class="fas fa-plus"/>
    </elevated-button>
  </div>
</template>
<script>
import TailwindInput from "@/components/TailwindInput";
import ElevatedButton from "@/components/ElevatedButton";

export default {
  components: { TailwindInput, ElevatedButton },
  data() {
    return { tarefa: "" };
  },
  methods: {
    submitTarefa: function() {
      this.$emit("submit", this.tarefa);
      this.tarefa = "";
    }
  }
};
</script>

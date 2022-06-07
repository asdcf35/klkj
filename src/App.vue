<template>
  <div id="app">
    <div class="container mx-auto py-10">
      <todo-list :list="orderedList" @create="create" @toggle="toggle" @remove="remove"/>
    </div>
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";

const saveToLocalStorage = data =>
  localStorage.setItem("state", JSON.stringify(data));
const loadFromLocalStorage = () =>
  JSON.parse(localStorage.getItem("state")) || [];
const by = field => (a, b) =>
  a[field] && !b[field] ? 1 : !a[field] && b[field] ? -1 : 0;

export default {
  name: "App",
  components: { TodoList },
  mounted() {
    this.list = loadFromLocalStorage();
  },
  computed: {
    orderedList: function() {
      return this.list.slice(0).sort(by("feita"));
    }
  },
  methods: {
    save: function() {
      saveToLocalStorage(this.list);
    },
    create: function(data) {
      if (data === "") return;
      const id = Math.random()
        .toString()
        .slice(2);
      const text = data;
      this.list.push({ id, text, feita: false });
      this.save();
    },
    toggle: function(id) {
      const idx = this.list.map(item => item.id).indexOf(id);
      if (idx < 0) {
        window.alert("não foi possível encontrar");
      } else {
        const list = this.list.slice(0);
        const item = list[idx];
        list[idx] = { ...item, ...{ feita: !item.feita } };
        this.list = list;
        this.save();
      }
    },
    remove: function(id) {
      this.list = this.list.filter(item => item.id !== id);
    }
  },
  data() {
    return {
      list: []
    };
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
textarea:focus,
input:focus {
  outline: none;
}
</style>

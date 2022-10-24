<template>
  <TodoList />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import TodoList from "./components/TodoList.vue";
import './styles/app.css'

export default defineComponent({
  name: "App",
  components: {
    TodoList,
  },
});
</script>
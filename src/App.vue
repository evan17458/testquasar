<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="bg-primary text-white">
      <q-toolbar>
        <q-toolbar-title> Quasar Todo List </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <q-page class="q-pa-md">
        <q-input
          v-model="newTodo"
          @keyup.enter="addTodo"
          label="新增待办事项"
          outlined
        >
          <template v-slot:append>
            <q-btn round dense flat icon="add" @click="addTodo" />
          </template>
        </q-input>

        <q-list separator bordered class="q-mt-md">
          <q-item
            v-for="(todo, index) in todos"
            :key="index"
            :class="{ done: todo.done }"
          >
            <q-item-section avatar>
              <q-checkbox v-model="todo.done" />
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ todo.text }}</q-item-label>
            </q-item-section>
            <q-item-section side>
              <q-btn
                flat
                round
                dense
                icon="delete"
                @click="removeTodo(index)"
              />
            </q-item-section>
          </q-item>
        </q-list>
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const newTodo = ref("");
    const todos = ref([]);

    const addTodo = () => {
      if (newTodo.value.trim().length > 0) {
        todos.value.push({
          text: newTodo.value.trim(),
          done: false,
        });
        newTodo.value = "";
      }
    };

    const removeTodo = (index) => {
      todos.value.splice(index, 1);
    };

    return {
      newTodo,
      todos,
      addTodo,
      removeTodo,
    };
  },
};
</script>

<style>
.done {
  text-decoration: line-through;
  color: #bbb;
}
</style>

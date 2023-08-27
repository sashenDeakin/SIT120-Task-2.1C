<script setup>
import { ref } from "vue";

const todoId = ref(0);
const todoItem = ref("");
const todoStore = ref([]);
const completed = ref(false);
const hoveredIndex = ref(null);

function addItems() {
  if (!todoItem.value) {
    alert("Please Enter Your Todo Item");
  } else {
    todoStore.value.push({
      id: todoId.value++,
      items: todoItem.value,
      status: completed.value,
      hoveredIndex: hoveredIndex,
    });

    todoItem.value = "";
  }
}

function toggleCompleted(idToFind) {
  const todo = this.todoStore.find((obj) => obj.id === idToFind);

  if (todo.status) {
    todo.status = false;
  } else {
    todo.status = true;
  }
}

function deleteTodo(idFind) {
  this.todoStore = this.todoStore.filter((item) => item.id !== idFind);
}
</script>

<template>
  <div class="todo-app">
    <header>
      <h1 class="header">Todo List</h1>
    </header>
    <main>
      <div class="add-todo">
        <input type="text" placeholder="Add a New Todo" v-model="todoItem" />
        <button @click="addItems">Add</button>
      </div>
      <ol class="todo-list">
        <li v-for="i in todoStore" :key="i.id" class="todo">
          <label class="checkbox">
            <input type="checkbox" @click="toggleCompleted(i.id)" />
            <span class="checkbox-custom"></span>
          </label>
          <span :class="{ completed: i.status }" class="todo-text">{{
            i.items
          }}</span>
          <button class="delete-button" @click="deleteTodo(i.id)">
            Delete
          </button>
        </li>
      </ol>
    </main>
  </div>
</template>

<style scoped>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}

.todo-app {
  max-width: 1000px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f8f8f8;
  align-items: center;
}

.header {
  font-size: 50px;
}

header {
  text-align: center;
  margin-bottom: 20px;
}

.add-todo {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.add-todo input[type="text"] {
  flex: 1;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 8px;
  height: 40px;
  font-size: 25px;
}

.add-todo button {
  padding: 8px 12px;
  background-color: #007bff;
  color: #fff;
  border: none;
  cursor: pointer;
  width: 100px;
  border-radius: 10px;
  font-size: 25px;
}

.add-todo button:hover {
  background-color: green;
  color: #fff;
}

.todo-list {
  list-style: none;
  padding: 0;
  cursor: pointer;
}

.hovered {
  background: red;
}

.todo {
  display: flex;
  align-items: center;
  padding: 10px;
  border: 1px solid #ccc;
  margin-bottom: 10px;
  border-radius: 5px;
}

.todo input[type="checkbox"] {
  margin-right: 10px;
}

.todo-text {
  flex: 1;
  font-size: 30px;
  font-weight: 700;
}

.delete-button {
  padding: 6px 12px;
  background-color: #ff4444;
  color: #fff;
  border: none;
  cursor: pointer;
  width: 100px;
  height: 40px;
  border-radius: 5px;
}

.completed {
  text-decoration: line-through;
}

.checkbox {
  display: flex;
  align-items: center;
  cursor: pointer;
}

.checkbox input[type="checkbox"] {
  display: none;
}

.checkbox-custom {
  width: 18px;
  height: 18px;
  border: 2px solid #ccc;
  border-radius: 3px;
  margin-right: 10px;
  position: relative;
}

.checkbox-custom::before {
  content: "";
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 10px;
  height: 10px;
  background-color: transparent;
  border-radius: 2px;
  transition: background-color 0.3s ease-in-out;
}

.checkbox input[type="checkbox"]:checked + .checkbox-custom::before {
  background-color: #007bff;
}

/* Media Queries */
@media screen and (max-width: 480px) {
  .todo-app {
    padding: 10px;
  }

  .add-todo {
    flex-direction: column;
    gap: 5px;
  }

  .add-todo input[type="text"] {
    width: 100%;
  }
}
</style>

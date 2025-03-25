<template>
  <div id="app">
    <div class="body-app">
      <h1>To-Do List</h1>
      <TaskFilter @filter="setFilter" />
      <TaskList :tasks="filteredTasks" @add-task="addTask" @edit-task="editTask" @delete-task="deleteTask" @toggle-task="toggleTask" />
    </div>
  </div>
</template>

<script>
import { computed, onMounted, ref } from 'vue';
import TaskFilter from './components/TaskFilter.vue';
import TaskList from './components/TaskList.vue';

export default {
  components: {
    TaskList,
    TaskFilter
  },
  setup() {
    const tasks = ref([]);
    const filter = ref('all');

    // Загрузка задач из LocalStorage
    onMounted(() => {
      const savedTasks = JSON.parse(localStorage.getItem('tasks')) || [];
      tasks.value = savedTasks;
    });

    // Сохранение задач в LocalStorage
    const saveTasks = () => {
      localStorage.setItem('tasks', JSON.stringify(tasks.value));
    };

    // Добавление задачи
    const addTask = (text) => {
      tasks.value.push({ id: Date.now(), text, completed: false });
      saveTasks();
    };

    // Редактирование задачи
    const editTask = (id, newText) => {
      const task = tasks.value.find(task => task.id === id);
      if (task) {
        task.text = newText;
        saveTasks();
      }
    };

    // Удаление задачи
    const deleteTask = (id) => {
      tasks.value = tasks.value.filter(task => task.id !== id);
      saveTasks();
    };

    // Переключение статуса задачи
    const toggleTask = (id) => {
      const task = tasks.value.find(task => task.id === id);
      if (task) {
        task.completed = !task.completed;
        saveTasks();
      }
    };

    // Фильтрация задач
    const filteredTasks = computed(() => {
      switch (filter.value) {
        case 'completed':
          return tasks.value.filter(task => task.completed);
        case 'active':
          return tasks.value.filter(task => !task.completed);
        default:
          return tasks.value;
      }
    });

    // Установка фильтра
    const setFilter = (newFilter) => {
      filter.value = newFilter;
    };

    return {
      tasks,
      filter,
      filteredTasks,
      addTask,
      editTask,
      deleteTask,
      toggleTask,
      setFilter
    };
  }
};
</script>

<style>
/* Базовые стили */
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

.body-app {
  text-align: center;
  border: 1px solid black;
  background-color: rgb(226, 226, 226);
  border-radius: 15px;
  max-width: fit-content;
  margin-inline: auto;
  margin-top: 60px;
  box-sizing: border-box;
}
</style>
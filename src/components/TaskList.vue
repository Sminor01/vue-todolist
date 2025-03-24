<template>
  <div>
    <input v-model="newTaskText" @keyup.enter="addTask" placeholder="Добавить задачу" />
    <button @click="addTask">Добавить</button>
    <div class="task-block">
      <TaskItem
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @edit-task="editTask"
        @delete-task="deleteTask"
        @toggle-task="toggleTask"
      />
  </div>
  </div>
</template>
  
<script>
import { ref } from 'vue';
import TaskItem from './TaskItem.vue';
export default {
  components: {
    TaskItem
  },
  props: {
    tasks: {
      type: Array,
      required: true
    }
  },
  emits: ['add-task', 'edit-task', 'delete-task', 'toggle-task'],
  setup(props, { emit }) {
    const newTaskText = ref('');
    const addTask = () => {
      if (newTaskText.value.trim()) {
        emit('add-task', newTaskText.value.trim());
        newTaskText.value = '';
      }
    };

    const editTask = (id, newText) => {
      emit('edit-task', id, newText);
    };

    const deleteTask = (id) => {
      emit('delete-task', id);
    };

    const toggleTask = (id) => {
      emit('toggle-task', id);
    };

    return {
      newTaskText,
      addTask,
      editTask,
      deleteTask,
      toggleTask
    };
  }
};
</script>

<style>
  .task-block {
    padding: 10px;
  }
</style>
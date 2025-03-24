<template>
    <li>
      <input
        type="checkbox"
        :checked="task.completed"
        @change="toggleTask(task.id)"
      />
      <span :class="{ completed: task.completed }">
        {{ task.text }}
      </span>
      <button @click="editTask(task.id)">Редактировать</button>
      <button @click="deleteTask(task.id)">Удалить</button>
    </li>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    props: {
      task: {
        type: Object,
        required: true
      }
    },
    emits: ['edit-task', 'delete-task', 'toggle-task'],
    setup(props, { emit }) {
      const isEditing = ref(false);
      const editedText = ref(props.task.text);
  
      const editTask = (id) => {
        const newText = prompt('Редактировать задачу:', props.task.text);
        if (newText !== null) {
          emit('edit-task', id, newText);
        }
      };
  
      const deleteTask = (id) => {
        emit('delete-task', id);
      };
  
      const toggleTask = (id) => {
        emit('toggle-task', id);
      };
  
      return {
        isEditing,
        editedText,
        editTask,
        deleteTask,
        toggleTask
      };
    }
  };
  </script>
  
  <style>
  .completed {
    text-decoration: line-through;
  }
  </style>
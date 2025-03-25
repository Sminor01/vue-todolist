<template>
  <div class="task">
    <div class="task-bnt">
      <button @click="editTask(task.id)">Редактировать</button>
      <button @click="deleteTask(task.id)">Удалить</button>
    </div>
    <div class="task-line">
      <input
        type="checkbox"
        :checked="task.completed"
        @change="toggleTask(task.id)"
      />
      <span :class="{ completed: task.completed }">
        {{ task.text }}
      </span>
    </div>
  </div>
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
  .task {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 200px;
    max-width: fit-content;
    border: 1px solid rgb(151, 151, 151);
    background-color: rgb(206, 206, 206);
    border-radius: 10px;
    margin-bottom: 10px;
  }
  .task-bnt {
    display: flex;
    flex-direction: row;
    justify-content: center;
    padding: 10px;
    gap: 10px;
  }
  .task-line {
    padding: 10px;
  }
</style>
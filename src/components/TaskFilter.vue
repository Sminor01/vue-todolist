<template>
    <div>
      <button @click="setFilter('all')">Все</button>
      <button @click="setFilter('active')">Активные</button>
      <button @click="setFilter('completed')">Выполненные</button>
    </div>
</template>
  
<script>
export default {
    emits: ['filter'],
    setup(props, { emit }) {
      const setFilter = (filter) => {
        emit('filter', filter);
      };
  
      return {
        setFilter
      };
    }
  };
</script>
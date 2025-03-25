<template>
    <div class="bnt-group">
      <button class="bntAll" @click="setFilter('all')">Все</button>
      <button class="bntACtive" @click="setFilter('active')">Активные</button>
      <button class="bntCompleted" @click="setFilter('completed')">Выполненные</button>
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

<style>
  .bnt-group {
    padding: 10px;
    display: flex;
    flex-direction: row;
    justify-content: center;
    gap: 15px;
    width: auto;
    height: auto;
  }
</style>
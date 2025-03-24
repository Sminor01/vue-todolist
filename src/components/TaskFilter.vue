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
  }
  .bntAll {
    padding: 10px;
  }
  .bntACtive{
    padding: 10px;
  }
  .bntCompleted {
    padding: 10px
  }

</style>
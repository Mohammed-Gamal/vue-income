<template>
  <div class="income-list">
    <IncomeItem 
      v-for="item in state.sortedIncome"
      :key="item.date"
      :income="item"
      @remove-item="$emit('remove-item', item.id)"
    />
  </div>
</template>

<script>
  import IncomeItem from '@/components/IncomeItem.vue'

  export default {
    props: {
      state: {
        type: Object,
        default: () => {}
      }
    },
    components: {
      IncomeItem
    }
  }
</script>

<style scoped>
  .income-list {
    margin: 30px;
    padding: 15px;
  }
</style>

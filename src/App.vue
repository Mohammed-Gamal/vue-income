<template>
  <MainHeader :totalIncome="state.totalIncome" />
  <MainForm @add-income="AddIncome" />
  <IncomeList :state="state" @remove-item="removeItem" />
</template>

<script>
  import { reactive, computed } from 'vue'
  import MainHeader from '@/components/MainHeader.vue'
  import MainForm from '@/components/MainForm.vue';
  import IncomeList from '@/components/IncomeList.vue';

  export default {
    components: {
      MainHeader,
      MainForm,
      IncomeList
    },
    setup() {
      const state = reactive({
        income: [],
        totalIncome: computed(() => {
          let temp = 0

          if (state.income.length > 0) {
            for (let i = 0; i < state.income.length; i++)
              temp += state.income[i].value
          }

          return temp
        }),
        sortedIncome: computed(() => {
          let si = [], temp = state.income

          si = temp.sort((a, b) => b.date - a.date)

          return si
        })
      })

      function AddIncome(data) {
        let d = data.date.split('-')
        let newD = new Date(d[0], d[1], d[2])

        state.income.push({
          id: Date.now(),
          desc: data.desc,
          value: data.value,
          date: newD.getTime()
        })

        console.log(state.income)
      }

      function removeItem(id) {
        state.income = state.income.filter(item => item.id !== id)
      }

      return {
        state,
        AddIncome,
        removeItem
      }
    }
  }
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Fira Sans', sans-serif;
  }

  body {
    background: #EEE;
  }
</style>

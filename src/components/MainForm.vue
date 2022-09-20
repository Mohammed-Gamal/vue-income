<template>
  <form @submit.prevent="handleForm">
    <input type="text" placeholder="Description..." v-model="formData.desc" />
    <input type="number" placeholder="Value..." v-model="formData.value" />
    <input type="date" placeholder="Date..." v-model="formData.date" />
    <button>Submit</button>
  </form>
</template>

<script>
  import { reactive } from 'vue'

  export default {
    props: {
      state: {
        type: Object,
        default: () => {}
      },
    },
    setup(props, { emit }) {
      const formData = reactive({
        desc: null,
        value: null,
        date: null
      })

      function handleForm() {
        emit('add-income', {
          desc: formData.desc,
          value: formData.value,
          date: formData.date
        })

        formData.desc = ''
        formData.value = ''
        formData.date = ''
      }

      return {
        formData,
        handleForm
      }
    }
  }
</script>

<style scoped>
  form {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    margin-top: 30px;
  }
  form input {
    font-size: 20px;
  }
  form input::placeholder {
    color: #AAA;
  }
  form input {
    display: block;
    padding: 5px 15px;
    outline: none;
    border: none;
    border-right: 1px solid #bbb;
    font-size: 20px;
    color: #888;
    background: #FFF;
  }
  form button {
    display: block;
    background: none;
    border: none;
    border-radius: 0px 8px 8px 0px;
    outline: none;
    color: #FFF;
    font-weight: 500;
    text-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
    padding: 5px 15px;
    background-color: #FFCE00;
    cursor: pointer;
  }
  form input:first-of-type {
    border-radius: 8px 0px 0px 8px;
  }
</style>
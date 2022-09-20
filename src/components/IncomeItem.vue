<template>
  <div class="income-item">
    <div class="removeItem" @click="$emit('remove-item', income.id)">&times;</div>
    <div class="desc">{{ income.desc }}</div>
    <div class="price">£{{ income.value }}</div>
    <div class="date">{{ fixDate() }}</div>
  </div>
</template>

<script>
  export default {
    props: {
      income: {
        type: Object
      }
    },
    setup(props) {
      function fixDate() {
        return new Date(props.income.date).toDateString()
      }

      return {
        fixDate
      }
    }
  }
</script>

<style scoped>
  .income-item {
    position: relative;
    display: flex;
    align-items: center;
    padding: 15px 10px;
    background-color: #FFF;
    border-radius: 8px;
    max-width: 600px;
    margin: 0 auto 15px;
  }

  .removeItem {
    color: #EF2D2D;
    font-weight: 600;
    font-size: 20px;
    line-height: 1;
    text-align: center;
    margin: 0 15px;
    cursor: pointer;
    transition: 0.3s;
  }

  .removeItem:hover {
    transform: scale(1.5);
  }

  .desc {
    color: #666;
    flex: 1 1 100%;
    font-size: 20px;
  }

  .price {
    color: #666;
    min-width: 100px;
    font-size: 20px;
  }

  .date {
    min-width: 120px;
    font-size: 14px;
    text-align: right;
    color: #666;
  }
</style>

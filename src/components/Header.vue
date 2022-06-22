<template>
  <div class="header">
      <div class="container">
          <h1 class="text-warning">{{ heading }}</h1>
          <h3>Score:  {{ numCorrect }} / {{ numTotal }} </h3>
      </div>
  </div>
</template>

<script>
export default {
  props: [
      'numCorrect',
      'numTotal',
      'heading'
  ]
}
</script>

<style scoped>
   .header{
       background-color: rgb(16, 16, 59);
       height: 20vh;
       display: flex;
       justify-content: space-between;
       align-items: center;
   }

   h1{
       font-size: 40px;
   }
</style>
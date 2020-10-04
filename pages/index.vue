<template>
   <div class="cnt">
      <div class="content">
         <h1>Форма - Кредитные и лизинговые программы</h1>
         <formL />
         <quiz />
      </div>
   </div>
</template>

<script>
   import formL from '~/components/form'
   import quiz from '~/components/quiz'

   export default {
      data: () => ({

      }),
      components: {
         formL,
         quiz
      }
   }
</script>

<style>
   .content {
      padding: 50px 0;

      h1 {
         margin-bottom: 30px;
      }
   }
</style>
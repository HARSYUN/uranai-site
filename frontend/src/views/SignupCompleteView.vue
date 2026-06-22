<template>

  <div class="container">

    <!-- ① タイトル -->
    <h1>占いのハウス</h1>
    <h2>新規会員登録</h2>

    <!-- ② メッセージ -->
    <p class="message">
      会員登録が完了しました<br>
      スタート画面へお戻りください
    </p>

    <!-- ③ ボタン -->
    <button @click="goStart">
      スタート画面へ
    </button>

  </div>

</template>


<script setup lang="ts">
  const emit = defineEmits<{
    (e: 'go', page: string): void
  }>()

  const goStart = () => {
    emit('go', 'start')
  }
</script>


<style scoped>
  .container {
    text-align: center;
    margin-top: 50px;
  }


  h1 {
    font-size: 4rem;
    margin-bottom: 80px; 
  }

  h2 {
    font-size: 2rem;
    margin-top: 0; 
    margin-bottom: 40px;
  }


  .message {
    margin: 30px 0;
    line-height: 2;
    color: #000;
  }

  
  button {
    display: block;
    width: 100%;
    max-width: 320px;
    margin: 30px auto;
    padding: 12px;
    font-size: 1.2rem;
    border-radius: 6px;
  }

</style>
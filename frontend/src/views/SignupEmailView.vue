<template>

  <div class="container">

    <!-- ① タイトル -->
    <h1>占いのハウス</h1>
    <h2>新規会員登録</h2>

    <!-- ② メッセージ -->
    <p class="message">
      メールアドレスに確認メールを送信しました<br>
      確認メールの内容の手順に従って本登録をお願いします<br>
      (仮サイトの文章です、実際にメールに届くわけではありません。)
    </p>

    <!-- ③ ボタン -->
    <button @click="goComplete">
      本登録する
    </button>

  </div>

</template>


<script setup lang="ts">
  const emit = defineEmits<{
    (e: 'go', page: string): void
  }>()

  const goComplete = () => {
    // 次の画面へ
    emit('go', 'signup_complete')
  }
</script>


<style scoped>
  .container {
    text-align: center;
    margin-top: 40px;
  }

  h1 {
    font-size: 4rem;
    margin-bottom: 80px;
  }

  h2 {
    font-size: 2rem;
    margin-bottom: 40px;
  }

  .message {
    margin: 40px 0;
    line-height: 2;
    color: #000;
  }

  button {
    display: block;
    width: 100%;
    max-width: 320px;
    margin: 30px auto;
    padding: 12px;
    font-size: 1.8rem;
    border-radius: 6px;
  }

</style>
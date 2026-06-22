<template>

  <div class="container">

    <!-- 共通ヘッダー枠（他ページと統一） -->
    <div class="header-buttons"></div>

      <!-- タイトル -->
      <h1 class="title">
        <span class="chunk">ようこそ　占いの</span>
        <span class="chunk">ハウスへ</span>
      </h1>


      <!--  ログイン -->
      <button class="login-btn" @click="goLogin">
        ログイン
      </button>

      <!--  新規登録 -->
      <button class="signup-btn" @click="goSignup">
        新規会員登録
      </button>

  </div>

</template>


<script setup lang="ts">

  const emit = defineEmits<{
    (e: 'go', page: string): void
  }>()

  const goLogin = () => {
    emit('go', 'login')
  }

  const goSignup = () => {
    emit('go', 'signup')
  }
</script>


<style scoped>

  /* 全体 */
  .container {
    text-align: center;
    margin-top: 60px;
    padding: 0 20px; 
  }

  /* ヘッダー */
  .header-buttons {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 90%;
    margin: 0 auto 20px;
  }

  /* タイトル */
  .title {
    font-size: 4rem;
    margin: 40px auto 80px;
    line-height: 1.4;
    text-align: center;
    white-space: nowrap; 
  }


  /* ボタン共通 */
  button {
    display: block;
    width: 100%;
    max-width: 320px;
    margin: 50px auto;
    padding: 12px;
    font-size: 1.5rem;
    border-radius: 6px;
  }

  /* 個別（微調整だけ） */
  .login-btn {
    margin-top: 20px;
  }

  .signup-btn {
    margin-top: 10px;
  }


  .chunk {
    white-space: nowrap; 
  }


  .br-sp {
    display: none;
  }


  /* スマホ版 */
  @media (max-width: 600px) {

    .title {
      font-size: 3rem;
      white-space: normal;   /* ←スマホだけ折り返しOK */
    }

    .br-sp {
      display: block;
    }
    
  }
    
  
</style>
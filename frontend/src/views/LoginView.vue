<template>

  <div class="container">

    <!-- 共通ボタンエリア -->
    <div class="header-buttons">
      <button class="back-btn" @click="goBack">
        前のページに戻る
      </button>
    </div>

    <!-- タイトル統一 -->
    <h1 class="main-title">占いのハウス</h1>
    <h2 class="sub-title">会員ログイン</h2>

    <label>メールアドレス</label>
    <input v-model="email" />

    <label>パスワード</label>
    <input type="password" v-model="password" />

    <p v-if="errorMessage" class="error">
      メールアドレスまたはパスワードが間違っています
    </p>

    <button @click="login">ログイン</button>

  </div>

</template>


<script setup lang="ts">
  import { ref } from 'vue'

  const emit = defineEmits<{
    (e: 'go', page: string): void
    (e: 'login-success', user: {
      name: string
      email: string
      gender: string
      birthdate: string
      created_at: string
    }): void
  }>()

  const email = ref('')
  const password = ref('')
  const errorMessage = ref(false)

  // ログイン
  const login = async () => {

    if (email.value === '' || password.value === '') {
      errorMessage.value = true
      return
    }

    try {
      const res = await fetch('http://localhost:3000/login', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          email: email.value,
          password: password.value
        })
      })

      const data = await res.json()

      
  if (data.success) {
    errorMessage.value = false

    // ユーザー情報を親に渡す
    emit('login-success', data.user)

    // 画面遷移
    emit('go', 'main')
  }
  else {
        errorMessage.value = true
      }

    } catch (error) {
      console.error(error)
      errorMessage.value = true
    }
  }

  // 戻る
  const goBack = () => {
    emit('go', 'start')
  }
</script>

<style scoped>

  /* 全体 */
  .container {
    text-align: center;
    margin-top: 0px; 
  }

  /* ボタン共通 */
  .header-buttons {
    display: flex;
    justify-content: flex-end;
    width: 90%;
    margin: 10px auto;
  }


  /* ボタン */
  button {
    display: block;
    width: 100%;
    max-width: 300px;
    margin: 30px auto;
    padding: 12px;
    font-size: 1.2rem;
    border-radius: 6px;
  }

  /* 戻るボタン */
  .back-btn {
    width: auto;
    max-width: none; 
    margin-right: 15%; 
  }


  /* タイトル */
  .main-title {
    font-size: 4rem;
    margin-bottom: 50px;
  }

  .sub-title {
    font-size: 2rem;
    margin-top: 0;
    margin-bottom: 40px;
  }

  label {
    color: #000;
    font-weight: bold;
  }

  /* 入力 */
  input {
    display: block;
    margin: 10px auto;
    padding: 8px;
    width: 100%;
    max-width: 300px;
    box-sizing: border-box;
    color: #000;
  }



  /* エラー */
  .error {
    color: red;
  }


  /* スマホ版 */
  @media (max-width: 600px) {
    .header-buttons {
      width: 100%;
      padding-right: 10px;
    }

    .back-btn {
      margin-right: 0;
    }
  }

</style>
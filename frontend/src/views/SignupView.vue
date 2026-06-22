<template>

  <div class="container">

    <!-- 共通ボタンエリア -->
    <div class="header-buttons">
      <button class="back-btn" @click="goBack">
        前のページに戻る
      </button>
    </div>

    <!-- タイトル（共通化） -->
    <h1 class="main-title">占いのハウス</h1>
    <h2 class="sub-title">新規会員登録</h2>

    <label>名前</label>
    <input v-model="name" placeholder="名前を入力してください" />

    <label>メールアドレス</label>
    <input v-model="email" placeholder="メールアドレスを入力してください" />

    <label>パスワード</label>
    <input
      type="password"
      v-model="password"
      placeholder="英数字8桁以上20桁未満"
    />

    <label>パスワード（確認用）</label>
    <input type="password" v-model="confirmPassword" />

    <label>性別</label>
    <select v-model="gender">
      <option value="">未選択</option>
      <option value="男">男</option>
      <option value="女">女</option>
      <option value="その他">その他</option>
    </select>

    <label>生年月日</label>
    <input type="date" v-model="birthdate" />

    <p v-if="passwordError" class="error">
      パスワードが条件を満たしていません
    </p>

    <p v-if="inputError" class="error">
      未入力の情報があります
    </p>

    <button class="submit-btn" @click="submit">  確認メール送信</button>

    </div>

  </template>


<script setup lang="ts">
  import { ref } from 'vue'

  const emit = defineEmits<{
    (e: 'go', page: string): void
  }>()

  const name = ref('')
  const email = ref('')
  const password = ref('')
  const confirmPassword = ref('')
  const gender = ref('')
  const birthdate = ref('')

  const passwordError = ref(false)
  const inputError = ref(false)

  const goBack = () => {
    emit('go', 'start')
  }

  
  const submit = async () => {

    passwordError.value = false
    inputError.value = false

    if (
      name.value === '' ||
      email.value === '' ||
      password.value === '' ||
      confirmPassword.value === '' ||
      birthdate.value === '' ||
      gender.value === ''
    ) {
      inputError.value = true
      return
    }

    if (
      password.value.length < 8 ||
      password.value.length >= 20 ||
      password.value !== confirmPassword.value
    ) {
      passwordError.value = true
      return
    }

    try {
      const res = await fetch('http://localhost:3000/register', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
        name: name.value,
        email: email.value,
        password: password.value,
        gender: gender.value,
        birthdate: birthdate.value
        })

      })

      const data = await res.json()

      if (res.ok) {
        //DB登録成功
        emit('go', 'signup_email')
      } else {
        alert(data.error)
      }

    } catch (error) {
      console.error(error)
      alert('サーバー接続エラー')
    }
  }

</script>


<style scoped>

  /* 全ページ統一 */
  .container {
    text-align: center;
    margin-top: 80px;  
  }

  /* 共通ヘッダー */
  .header-buttons {
  display: flex;
  justify-content: flex-end;
  width: 90%;
  margin: -40px auto;
  }

  /* 戻るボタン */
  .back-btn {
  margin-right: 15%; 
  }

  /* タイトル */
  .main-title {
    font-size: 64px;
    margin-top: 70px;
    margin-bottom: 50px;
  }

  /* サブタイトル */
  .sub-title {
    font-size: 32px;
    margin-bottom: 40px;
  }


  label {
    color: #000;  
    font-weight: bold; 
  }

  input::placeholder {
    color: #000; 
    opacity: 1; 
  }


  /* 入力 */
  input, select {
    display: block;
    margin: 10px auto;
    padding: 8px;
    width: 100%; 
    max-width: 300px;
    box-sizing: border-box;
  }

  /* ボタン共通 */
  button {
    display: block;
    width: 100%;
    max-width: 240px;
    margin: 20px auto;
    padding: 12px;
    font-size: 1.2rem;
    border-radius: 6px;
  }

  .submit-btn {
  margin-top: 40px;  
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
    margin: 10px auto;
  }

  .back-btn {
    margin-right: 0; 
  }

}

</style>
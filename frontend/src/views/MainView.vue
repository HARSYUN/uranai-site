<template>

  <div class="container">

    <!-- ヘッダー -->
    <div class="header-buttons">

      <!-- ユーザー名 -->
      <p class="user">{{ user.name }}様</p>

      <!-- 右ボタン -->
      <div class="right">
        <button class="btn mypage-btn" @click="goMyPage">
          マイページへ
        </button>

        <button class="btn logout-btn" @click="logout">
          ログアウト
        </button>
      </div>

    </div>

    <!-- タイトル -->
    <h1 class="main-title">占いのハウス</h1>

    <!-- メインボタン -->
    <button class="btn uranai-btn" @click="goResult">
      今日の運勢を占う
    </button>

  </div>

</template>


<script setup lang="ts">

  // props
  const props = defineProps<{
    user: {
      name: string
      email: string
      password: string
    }
  }>()

  // emit
  const emit = defineEmits<{
    (e: 'go', page: string): void
  }>()

  const user = props.user

  // マイページ
  const goMyPage = () => {
    emit('go', 'mypage')
  }

  // ログアウト
  const logout = () => {
    localStorage.removeItem('user')
    emit('go', 'start')
  }

  // 占い結果
  const goResult = () => {
    emit('go', 'main_result')
  }

</script>


<style scoped>

  /* 全体 */
  .container {
    text-align: center;
    margin-top: 40px;
  }


  /* ヘッダー */
  .header-buttons {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 90%;
    margin: 10px auto;
  }

  .user {
    font-weight: bold;
    font-size: 20px;
    white-space: nowrap;
  }

  .right {
    display: flex;
    gap: 20px;
    flex-wrap: wrap;
  }


  /* ボタン共通 */
  .btn {
    padding: 12px;
    font-size: 1rem;
    border-radius: 6px;
  }


  /* ヘッダーボタン */
  .mypage-btn,
  .logout-btn {
    width: auto;
    padding: 12px 20px;
  }


  /* メインボタン */
  .uranai-btn {
    display: block;
    width: 100%;
    max-width: 320px;
    margin: 30px auto;
    font-size: 1.2rem;
  }


  /* タイトル */
  .main-title {
    font-size: 4rem;
    margin: 80px 0;
  }


  /* スマホ版 */
  @media (max-width: 600px) {

    .header-buttons {
      flex-direction: column;
      align-items: flex-start;
    }

    .right {
      width: 100%;
    }

  }

</style>
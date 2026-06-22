<template>
  <div class="container">

    <!-- 上に移動 -->
    <div class="header-buttons">

      <!-- 左 -->
      <p class="user">{{ user.name }}様</p>

      <!-- 右 -->
      <div class="right">
        <button class="btn back-btn" @click="goBack">
          前のページへ戻る
        </button>

        <button class="btn logout-btn" @click="logout">
          ログアウト
        </button>
      </div>

    </div>


    <!-- タイトル -->
      <h1 class="main-title">占いのハウス</h1>
      <h2 class="sub-title">マイページ</h2>

    <!-- 下に移動 -->
    <div class="profile">
      <p>名前：{{ user.name }}</p>
      <p>メール：{{ user.email }}</p>
      <p>性別：{{ user.gender }}</p>
      <p>誕生日：{{ user.birthdate }}</p>
      <p>登録日：{{ formatDate(user.created_at) }}</p>
    </div>

  </div>
</template>


<script setup lang="ts">

    const props = defineProps<{
    user: {
        name: string
        email: string
        gender: string
        birthdate: string
        created_at: string
    }
    }>()

    /* 登録日 */
    const formatDate = (dateStr: string) => {
      const date = new Date(dateStr)

      const y = date.getFullYear()
      const m = date.getMonth() + 1
      const d = date.getDate()

      return `${y}/${m}/${d}`
    }

    const emit = defineEmits<{
    (e: 'go', page: string): void
    }>()

    const user = props.user

    const goBack = () => {
    emit('go', 'main')
    }

    const logout = () => {
    localStorage.removeItem('user')
    emit('go', 'start')
    }

</script>


<style scoped>

  /* ヘッダー */
  .header-buttons {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 90%; 
    margin: 50px auto; 
  }

  .main-title {
    font-size: 4rem;
    margin-top: 40px;
    margin-bottom: 60px;
  }

  .sub-title {
    font-size: 3rem;
    margin-bottom: 40px;
  }

  /* ユーザー名 */
  .user {
    font-weight: bold;
    font-size: 20px;
  }

  /* 右側 */
  .header-buttons .right {
    display: flex;
    gap: 20px;
  }

  /* 共通ボタン*/
  .btn {
    display: inline-block;
    padding: 12px 20px;
    font-size: 1rem;
    border-radius: 6px;
  }

  /*  個別ボタン調整 */
  .back-btn,
  .logout-btn {
    width: auto;
  }


  /* プロフィール */
  .profile {
    margin-top: 40px;
    font-size: 1.2rem; 
    line-height: 2; 
    color: #000;
  }

  

</style>
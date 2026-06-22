<template>

  <div class="container">

    <!-- 共通ヘッダー -->
    <div class="header-buttons">
      <button class="btn back-btn" @click="goBack">
        前のページに戻る
      </button>

      <button class="btn logout-btn" @click="logout">
        ログアウト
      </button>
    </div>

    <!-- タイトル統一 -->
    <h1 class="main-title">占いのハウス</h1>
    <h2 class="sub-title">占い結果</h2>

    <!-- 結果 -->
    <p class="result">
      今日の運勢は…
    </p>

    <h2 :class="['result-text', getResultClass()]">
      {{ result }}
    </h2>

    <!-- 再抽選 -->
    <button class="btn retry" @click="draw">
      もう一度占う
    </button>

  </div>

</template>


<script setup lang="ts">

  import { ref, onMounted } from 'vue'

  // emit
  const emit = defineEmits<{
    (e: 'go', page: string): void
  }>()

  // 結果
  const result = ref('')

  const getResultClass = () => {

    if (result.value.includes('吉')) {
      return 'good'   // 赤
    }

    if (result.value.includes('凶')) {
      return 'bad'    // 青
    }

    return ''
  }

  // 占い
  const draw = () => {
    const list = ['大吉', '中吉', '小吉', '吉', '凶', '小凶', '中凶', '大吉']
    const index = Math.floor(Math.random() * list.length)
    result.value = list[index]
  }

  // 初回実行
  onMounted(() => {
    draw()
  })

  // 戻る
  const goBack = () => {
    emit('go', 'main')
  }

  // ログアウト
  const logout = () => {
    emit('go', 'start')
  }
</script>


<style scoped>

  /* 全体 */
  .container {
    text-align: center;
    margin-top: 80px;
  }

   /* ヘッダー */
  .header-buttons {
    display: flex;
    justify-content: flex-end;
    gap: 20px;
    width: 90%;
    margin: -30px auto;
  }


  /* ボタン共通 */
  .btn {
    padding: 12px 20px;
    font-size: 1rem;
    border-radius: 6px;
  }

    .back-btn,
  .logout-btn {
    width: auto;
    padding: 10px 20px;
  }

  .retry {
    display: block;
    width: 100%;
    max-width: 320px;
    margin: 40px auto;
    font-size: 1.2rem;
  }


  /* タイトル */
  .main-title {
    font-size: 4rem;
    margin-top: 100px;
    margin-bottom: 50px;
  }

  /* サブタイトル */
  .sub-title {
    font-size: 2rem;
    margin-top: 0;
    margin-bottom: 40px;
  }


  /* 「今日の運勢は…」 */
  .result {
    margin-top: 0px;  
    margin-bottom: 40px; 
    font-size: 32px;
    color: #000;
  }

  .result-text {
    font-size: 64px;
    margin-top: 10px;
  }


  .good {
    color: red;
  }

  .bad {
    color: blue;
  }


  /* もう一度占うボタン */
  .retry {
    margin-top: 40px;
    padding: 12px 30px;
  }
  
</style>
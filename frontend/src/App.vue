<template>
  <StartView v-if="page === 'start'" @go="changePage" />

  <LoginView
    v-if="page === 'login'"
    @go="changePage"
    @login-success="updateUser"
  />


  <SignupView
    v-if="page === 'signup'"
    @go="changePage"
    @register="saveUser"
  />

  <SignupEmailView
    v-if="page === 'signup_email'"
    @go="changePage"
  />

  <SignupCompleteView
    v-if="page === 'signup_complete'"
    @go="changePage"
  />

  <MainView
    v-if="page === 'main'"
    @go="changePage"
    :user="user"
  />

  <MainResultView 
    v-if="page === 'main_result'" @go="changePage" 
  />

  <MyPageView
    v-if="page === 'mypage'"
    @go="changePage"
    :user="user"
  />

</template>


<script setup lang="ts">
  import { ref, onMounted } from 'vue'

  import StartView from './views/StartView.vue'
  import LoginView from './views/LoginView.vue'

  import SignupView from './views/SignupView.vue'
  import SignupEmailView from './views/SignupEmailView.vue'
  import SignupCompleteView from './views/SignupCompleteView.vue'

  import MainView from './views/MainView.vue'
  import MainResultView from './views/MainResultView.vue'
  import MyPageView from './views/MyPageView.vue'

  const page = ref('start')

  // ユーザー情報
  const user = ref({
    name: '',
    email: '',
    password: '',
    gender: '',
    birthdate: '',
    created_at: ''
  })

  const changePage = (next: string) => {
    page.value = next
  }

  // 登録情報保存
  const saveUser = (data: any) => {
    user.value.name = data.name
    user.value.email = data.email
    user.value.password = data.password
  }

  
const updateUser = (data: any) => {
  user.value.name = data.name
  user.value.email = data.email
  user.value.gender = data.gender
  user.value.birthdate = data.birthdate
  user.value.created_at = data.created_at


  //ログイン状態保存.
  localStorage.setItem('user', JSON.stringify(user.value))
  }

  onMounted(() => {
    const saved = localStorage.getItem('user')

    if (saved) {
      const parsed = JSON.parse(saved)

      user.value.name = parsed.name
      user.value.email = parsed.email

      page.value = 'main'
    }
  })
  
</script>
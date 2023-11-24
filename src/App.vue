<script setup lang="ts">
import { onMounted, ref } from 'vue'
import TheFlex from './components/TheFlex.vue'

const isDarkMode = ref<string>('')

function changeColor() {
  if (isDarkMode.value === 'light') {
    document.documentElement.classList.remove('light')
    document.documentElement.classList.add('dark')
    document.cookie = 'darkMode=dark'
    isDarkMode.value = 'dark'
  } else {
    document.documentElement.classList.remove('dark')
    document.documentElement.classList.add('light')
    document.cookie = 'darkMode=light'
    isDarkMode.value = 'light'
  }
  console.log(document.cookie)
}

function getCookie(name: string) {
  let cookieArray = document.cookie.split(';')
  for (let i = 0; i < cookieArray.length; i++) {
    let cookie = cookieArray[i]
    while (cookie.charAt(0) == ' ') {
      cookie = cookie.substring(1)
    }
    if (cookie.indexOf(name) == 0) {
      return cookie.substring(name.length + 1)
    }
  }
  return ''
}

onMounted(() => {
  isDarkMode.value = getCookie('darkMode')
  if (isDarkMode.value === 'dark') {
    document.documentElement.classList.add('dark')
    return
  }
  document.documentElement.classList.add('light')
})
</script>

<template>
  <main class="dark:bg-dark-500 light:bg-light-500 min-h-screen duration-300">
    <h1
      class="text-8 md:text-12 lg:text-14 xl:text-16 light:text-black cursor-pointer bg-blue-900 py-[20px] text-center transition ease-in-out hover:bg-green-500 hover:text-red-600 dark:text-white"
    >
      UnoCss 初體驗
    </h1>
    <p class="light:text-black mt-1 dark:text-white">
      基本上就是測試各種用法，沒有實際邏輯在跑的Playground
    </p>
    <button
      class="px10 light:bg-gray-300 light:text-dark rounded-50 border-1 mx-auto my-10 block cursor-pointer py-5 hover:bg-indigo-500 dark:bg-purple-600 dark:text-white"
      @click="changeColor"
    >
      切換日夜間模式
    </button>
    <TheFlex />
  </main>
</template>

<style scoped></style>

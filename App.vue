<template>
  <div>
    <header class="header-hero">
      <div class="site-container">
        <div class="navbar">
          <div class="logo"><img :src="logoSrc" alt="logo"/><div><div class="font-bold">{{ t('app.name') }}</div><div class="text-sm">{{ t('app.team') }}</div></div></div>
          <div class="flex items-center gap-3">
            <div class="search-bar hidden sm:flex"><input placeholder="ابحث عن مدرسة، محافظة..." class="outline-none"/><button class="cta">Search</button></div>
            <button @click="toggleTheme" class="btn">{{ isDark ? t('app.light') : t('app.dark') }}</button>
            <select v-model="locale" @change="switchLocale" class="btn">
              <option value="ar">العربية</option><option value="en">English</option>
            </select>
            <router-link to="/profile" class="cta">{{ t('home.cta') }}</router-link>
          </div>
        </div>
        <div class="hero-grid mt-6">
          <div>
            <h1 class="text-4xl font-extrabold leading-tight">{{ t('home.headline') }}</h1>
            <p class="mt-3 text-lg opacity-90">{{ t('home.sub') }}</p>
            <div class="features mt-6">
              <div class="card"><strong>1</strong><div class="mt-2">{{ t('home.features')[0] }}</div></div>
              <div class="card"><strong>2</strong><div class="mt-2">{{ t('home.features')[1] }}</div></div>
              <div class="card"><strong>3</strong><div class="mt-2">{{ t('home.features')[2] }}</div></div>
              <div class="card"><strong>4</strong><div class="mt-2">{{ t('home.features')[3] }}</div></div>
            </div>
          </div>
          <div class="card">
            <img :src="logoSrc" class="w-full h-auto" alt="visual"/>
          </div>
        </div>
      </div>
    </header>
    <main class="site-container section"><router-view/></main>
    <footer class="footer"><div class="site-container"><div class="flex justify-between items-center"><div><strong>EduVision — EduMasr</strong><p class="kicker">© 2025</p></div></div></div></footer>
  </div>
</template>
<script setup>
import { computed, ref } from 'vue'
import { useI18n } from './plugins/i18n.js'
import { auth } from './composables/auth.js'
const { t, locale } = useI18n()
const isDark = ref(localStorage.getItem('theme')==='dark')
function toggleTheme(){ isDark.value=!isDark.value; localStorage.setItem('theme', isDark.value?'dark':'light'); document.documentElement.classList.toggle('dark', isDark.value) }
function switchLocale(){ localStorage.setItem('locale', locale.value); document.documentElement.setAttribute('dir', locale.value==='ar'?'rtl':'ltr') }
const user = computed(()=> auth.currentUser())
const logoSrc = computed(()=> document.documentElement.classList.contains('dark') ? '/src/assets/logo-dark.png' : '/src/assets/logo-light.png')
</script>

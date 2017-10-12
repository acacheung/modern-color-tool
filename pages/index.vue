<template>
  <div id="app">
    <app-header></app-header>
    <div class="colors">
      <h2 class="t-hidden">Colors</h2>
      <h3 class="heading">
        Primary color:
        <input class="input--primary" type="color" v-model="primary">
      </h3>
      <div class="color background-color--primary"></div>
      <h3 class="heading">
        Secondary color:
        <input class="input--secondary" type="color" v-model="secondary">
      </h3>
      <div class="color background-color--secondary"></div>
    </div>
    <div class="layouts">
      <p class="t-text">Find your palette according to proportion and relationships.</p>
      <div class="layout background-color--primary">
        <svg class="fill--secondary" viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
          <circle cx="100" cy="100" r="50"/>
        </svg>
      </div>
      <div class="layout background-color--primary">
        <svg class="fill--secondary" viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
          <path d="M 100,40 160,150 40,150 z"/>
        </svg>
      </div>
      <div class="layout background-color--primary">
        <svg class="fill--secondary" viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
          <rect x="55" y="55" width="90" height="90"/>
        </svg>
      </div>
    </div>
  </div>
</template>

<script>
  import AppHeader from '@/components/AppHeader'
  export default {
    components: {
      AppHeader
    },
    data: function () {
      return {
        primary: '#ebb8f8',
        secondary: '#5938ff'
      }
    },
    watch: {
      primary (value) {
        this.$el.style.setProperty('--primary', value)
      },
      secondary (value) {
        this.$el.style.setProperty('--secondary', value)
      }
    }
  }
</script>

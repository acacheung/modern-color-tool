<template>
  <div id="app">
    <app-header></app-header>
    <canvas id="favicon"></canvas>
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
  import _ from 'lodash'
  export default {
    components: {
      AppHeader
    },
    data: function () {
      return {
        primary: '',
        secondary: ''
      }
    },
    created: function () {
      if (this.$route.hash) {
        var colors = this.$route.hash.slice(1).split('-')
        this.primary = '#' + colors[0]
        this.secondary = '#' + colors[1]
      } else {
        this.primary = '#ebb8f8'
        this.secondary = '#5938ff'
      }
    },
    methods: {
      slowDownRouterPush: _.throttle(function () {
        this.$router.push(this.primary + '-' + this.secondary.substr(1))
      }, 500),
      updateFavicon: function () {
        var canvas = document.getElementById('favicon')
        var ctx = canvas.getContext('2d')
        canvas.width = canvas.height = 32
        ctx.beginPath()
        ctx.arc(16, 16, 16, 0, 2 * Math.PI, false)
        ctx.clip()
        ctx.fillStyle = this.primary
        ctx.fillRect(0, 0, 16, 32)
        ctx.fillStyle = this.secondary
        ctx.fillRect(16, 0, 16, 32)
        var dataURL = canvas.toDataURL()
        document.querySelector('link[rel="icon"]').setAttribute('href', dataURL)
      }
    },
    watch: {
      primary (value) {
        document.documentElement.style.setProperty('--primary', value)
        this.slowDownRouterPush()
        this.updateFavicon()
      },
      secondary (value) {
        document.documentElement.style.setProperty('--secondary', value)
        this.slowDownRouterPush()
        this.updateFavicon()
      }
    }
  }
</script>

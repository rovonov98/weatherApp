<template>
  <div class="app">
    <Weather />
  </div>
</template>

<script>
import Weather from './components/Weather'
export default {
    components: {
      Weather
    }
  }
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
@media(max-width: 576px) {
    :root {
      font-size: 12px;
    }
  }
  @media(min-width: 576px) {
    :root {
      font-size: 14px;
    }
  }
  @media(min-width: 768px) {
    :root {
      font-size: 15px;
    }
  }
  @media(min-width: 992px) {
    :root {
      font-size: 16px;
    }
  }
  @media(min-width: 1200x) {
    :root {
      font-size: 16px;
    }
  }
</style>

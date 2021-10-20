<template>
  <div class='footer-div'>
    <div class='footer-container'>
      <div style='margin-bottom: 0.5rem'>Copyright © 2020 - <span id='copy-year'>2021</span> <a class='footer-link' href='/'>Neekko33's Blog</a></div>
      <div>Powered by <a class='footer-link' href='https://nuxtjs.org/' rel='external nofollow noopener noreferrer'
                         target='_blank'>Nuxt.js</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Footer'
}
</script>

<style scoped>
.footer-div {
  background-color: #fff;
  box-shadow: 0 4px 10px rgba(0, 2, 4, 0.06), 0 0 1px rgba(0, 2, 4, 0.11);;
  color: #6b7f94;;
  contain: content;
  display: block;
  padding: 3rem 1.5rem 3rem;
  text-align: center;
}

@media screen and (min-width: 768px) {
  .footer-container {
    justify-content: space-between;
  }
}


.footer-container {
  flex-grow: 1;
  margin: 0 auto;
}
</style>

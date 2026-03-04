<template>
  <footer class="footer">
    <div class="footer-content">
      <p class="footer-text">
        © {{ year }} Idriz Mitiam. All rights reserved.
      </p>
    </div>
  </footer>
</template>

<script setup>
const year = new Date().getFullYear();
</script>

<style scoped>
.footer {
  background-color: #000;
  color: white;
  padding: 24px 0;
  margin-top: 4rem;
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1.5rem;
  text-align: center;
}

.footer-text {
  font-family: 'Poppins', sans-serif;
  font-size: 0.95rem;
  opacity: 0.85;
}
</style>

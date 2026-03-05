<script setup>
const user = {
  name: 'Idriz Mitiam',
  bio: 'Passionate Web Developer & UI/UX Designer.',
  photo: 'https://via.placeholder.com/100',
  social: {
    github: 'https://github.com/yourprofile',
    linkedin: 'https://linkedin.com/in/yourprofile',
  }
}

const projects = [
  { title: 'Project One', image: 'https://via.placeholder.com/150', description: 'A cool project.' },
  { title: 'Project Two', image: 'https://via.placeholder.com/150', description: 'Another awesome work.' },
]

const year = new Date().getFullYear()
</script>

<template>
  <div class="layout">
    <!-- Top Navigation -->
    <nav class="navbar">
      <div class="nav-brand">PORTFOLIO</div>
      <ul class="nav-links">
        <li>{{ user.name }}</li>
      </ul>
    </nav>

    <!-- Main Content -->
    <main class="router-outlet">
      <router-view />
    </main>

    <!-- Footer -->
    <footer class="footer">
      <p class="footer-text">© {{ year }} {{ user.name }}. Coded in Vue.</p>
    </footer>
  </div>
</template>

<style scoped>
.layout {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

/* NAVBAR */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: black;
  padding: 15px 40px;
  color: white;
}

.nav-brand {
  font-family: 'Poppins', sans-serif;
  font-size: 1.2rem;
  font-weight: bold;
}

.nav-links {
  list-style: none;
  font-family: 'Poppins', sans-serif;
  font-size: 1.2rem;
  margin: 0;
  padding: 0;
}

/* MAIN CONTENT */
.router-outlet {
  flex: 1;
  padding: 20px;
  background: #f3f4f6;
}

/* FOOTER */
.footer {
  background-color: black;
  
  padding: 18px 40px;
 
 
}

.footer-text {
  position: relative;
  color: white;
  font-family: 'Poppins', sans-serif;
  font-size: 1.2rem;
  top: -0.08rem;
  text-align: center;  /* text aligned to right corner */
  margin: 0;
}
@media (max-width: 430px) { 

  .footer {
 position: absolute !important;
 margin-top: 133.5rem !important;
 width: 30rem !important;
  }
.footer-text {
  left: -2rem !important;
}
  .footer-text,
  .nav-links,
  .nav-brand {
    font-size: 0.9rem;
  }
}

@media (max-width: 320px) { 

  .footer-text,
  .nav-links,
  .nav-brand {
    font-size: 0.9rem;
  }
}

</style>

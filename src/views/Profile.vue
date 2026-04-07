<script setup>
import { ref, onMounted, nextTick, watch, computed, onBeforeUnmount   } from 'vue';
import yImg from '@/assets/y.png';
import ijmImg from '@/assets/I.png';
import bg1 from "@/assets/work1.png";
import bg2 from "@/assets/work2.png";
import bg3 from "@/assets/work3.png";
import bg4 from "@/assets/work4.png";
import bg5 from "@/assets/work5.png";



/* user data */
const user = {
  name: 'Your Name',
  bio: 'Passionate Web Developer & UI/UX Designer.',
  photo: ijmImg,
  facebook: 'https://www.facebook.com/idrizjoaquin.mitiam/',
  linkedin: 'https://www.linkedin.com/in/idriz-mitiam-271946219',
  github: 'https://github.com/Zidri',
};

const user1 = {
  name: 'Your Name',
  bio: 'Passionate Web Developer & UI/UX Designer.',
  photo: yImg,
  facebook: 'https://www.facebook.com/idrizjoaquin.mitiam/',
  linkedin: 'https://www.linkedin.com/in/idriz-mitiam-271946219',
  github: 'https://github.com/Idrizzzz',
};

/* projects */
const projects = [
  {
    title: 'Project One',
    image: 'https://via.placeholder.com/150',
    description: 'A cool project.',
  },
  {
    title: 'Project Two',
    image: 'https://via.placeholder.com/150',
    description: 'Another awesome work.',
  },
];

/* pagination state */
const page = ref(1);
const totalPages = 2;

/* pagination methods */
const nextPage = () => {
  if (page.value < totalPages) page.value++;
};

const prevPage = () => {
  if (page.value > 1) page.value--;
};



const pageStatus = ref(1);
const totalStatus = 2;

// Track direction: 'left' for next, 'right' for prev
const transitionName = ref("fade");

const nextStatus = () => {
  if (pageStatus.value < totalStatus) {
   
    pageStatus.value++;
  }
};

const prevStatus = () => {
  if (pageStatus.value > 1) {
    
    pageStatus.value--;
  }
};

const showPage = ref(false);

onMounted(() => {
  showPage.value = true;
});

const skillsVisible = ref(false);

onMounted(() => {
  nextTick(() => {
    const skillsEl = document.querySelector('.skills');
    if (!skillsEl) return;

    const observer = new IntersectionObserver(
      ([entry]) => {
        skillsVisible.value = entry.isIntersecting;
      },
      {
        threshold: 0.2 // triggers when 50% of element is visible
      }
    );

    observer.observe(skillsEl);
  });
});



// Slide state
const activeSlide = ref(1);
const totalSlides = 5;

// ----------------------
// DESKTOP BACKGROUNDS
// ----------------------
const slideBackgroundsDesktop = [
  new URL("@/assets/work1.png", import.meta.url).href,
  new URL("@/assets/work2.png", import.meta.url).href,
  new URL("@/assets/work3.png", import.meta.url).href,
  new URL("@/assets/work4.png", import.meta.url).href,
  new URL("@/assets/work5.png", import.meta.url).href,
];

// ----------------------
// MOBILE BACKGROUNDS
// ----------------------
const slideBackgroundsMobile = [
  new URL("@/assets/work1-mobile.png", import.meta.url).href,
  new URL("@/assets/work2-mobile.png", import.meta.url).href,
  new URL("@/assets/work3-mobile.png", import.meta.url).href,
  new URL("@/assets/work4-mobile.png", import.meta.url).href,
  new URL("@/assets/work5-mobile.png", import.meta.url).href,
];

// ----------------------
// SCREEN DETECTION
// ----------------------
const isMobile = ref(window.innerWidth <= 768);

const checkScreen = () => {
  isMobile.value = window.innerWidth <= 768;
};

// ----------------------
// ACTIVE BACKGROUND
// ----------------------
const activeBackground = computed(() => {
  const slides = isMobile.value
    ? slideBackgroundsMobile
    : slideBackgroundsDesktop;

  return slides[activeSlide.value - 1];
});

// ----------------------
// TRANSITION
// ----------------------
const slideTransition = ref("slide-left");

// ----------------------
// SLIDESHOW
// ----------------------
let slideInterval = null;
const slideDelay = 6000;

// Next slide
const nextSlide = async () => {
  slideTransition.value = "slide-left";

  await nextTick();
  activeSlide.value =
    activeSlide.value >= totalSlides ? 1 : activeSlide.value + 1;

  restartSlideshow();
};

// Previous slide
const prevSlide = async () => {
  slideTransition.value = "slide-right";

  await nextTick();
  activeSlide.value =
    activeSlide.value <= 1 ? totalSlides : activeSlide.value - 1;

  restartSlideshow();
};

// Start auto slideshow
const startSlideshow = () => {
  stopSlideshow();
  slideInterval = setInterval(() => {
    slideTransition.value = "slide-left";
    activeSlide.value =
      activeSlide.value >= totalSlides ? 1 : activeSlide.value + 1;
  }, slideDelay);
};

// Stop slideshow
const stopSlideshow = () => {
  if (slideInterval) {
    clearInterval(slideInterval);
    slideInterval = null;
  }
};

// Restart after manual click
const restartSlideshow = () => {
  stopSlideshow();
  startSlideshow();
};

// ----------------------
// LIFECYCLE
// ----------------------
onMounted(() => {
  window.addEventListener("resize", checkScreen);
  startSlideshow();
});

onBeforeUnmount(() => {
  window.removeEventListener("resize", checkScreen);
  stopSlideshow();
});

</script>



<template>
  <Transition name="page-fade" appear>
    <div v-if="showPage" class="main1">
      <div class="grid">
 
      <!-- Card 1: Welcome -->
      <div class="card1">
        <p class="hi">Hi I'm Idriz!👋</p>
      </div>

      <div class="card3">
        <h6 class="perspect">Unlock Fresh Perspectives!</h6>
        <h6 class="perspect1">Through Innovative Web</h6>
      </div>

      <!-- Card 2: More About Me -->
      <div class="card2">
        <h3>More About Me</h3>
        <div class="underline"></div>
        <Transition name="fade" mode="out-in">
          <p v-if="page === 1">
           I am a graduate of the Polytechnic University of  
           the Philippines (PUP), 
           <span class="mobile-br"></span>
           where I earned a  bachelor’s degree
           <span class="mobile-br"></span>
            in  Computer Engineering. 
           
         I also hold a  diploma degree in the same field.
          </p>
          <p v-else-if="page === 2">
            I enjoy exploring UI/UX design using Figma and Adobe XD, experimenting
            with clean and user-friendly interfaces.
            <br /><br />
            I’m also passionate about web development with React.js and Vue.js,
            where I like to create interactive and responsive web experiences.
          </p>
        </Transition>

        <!-- Pagination buttons -->
        <div class="pagination corner">
          <button @click="prevPage" :disabled="page === 1">&lt;</button>
          <span class="page-number">{{ page }}</span>
          <button @click="nextPage" :disabled="page === totalPages">&gt;</button>
        </div>
      </div>

      <!-- Card 3: Profile Image -->
      <div class="ijm">
        <img :src="user.photo" alt="Profile" class="ijm" />
      </div>

      <!-- Card 4: Social Links -->
      <div class="card">
        <div class="social-links">
          <a :href="user.facebook" target="_blank" aria-label="Facebook">
            <i class="fab fa-facebook"></i>
          </a>
          <a :href="user.linkedin" target="_blank" aria-label="LinkedIn">
            <i class="fab fa-linkedin"></i>
          </a>
          <a :href="user.github" target="_blank" aria-label="GitHub">
            <i class="fab fa-github"></i>
          </a>
        </div>
      </div>

      <!-- Card 5: Industry Experience -->
      <div class="card4">
        <div class="title-box">
          <h3>Industry Experience</h3>
        </div>

        <h3>{{ pageStatus === 1 ? "Recently" : "Currently" }}</h3>

       <Transition :name="transitionName" mode="out-in">
  <div v-if="pageStatus === 1" key="1">
    <p class="industry">
      LexMeet, Inc: April 2022 - Aug 2022, Web Development Intern (React.js & PHP Laravel)
    </p>
    <p class="industry1">
      The Programmers' Guild (PUP TPG): Oct 2024 - Oct 2025, Assistant Vice President of Records
    </p>
     <p class="industry2">
     Google Developer Group (GDG) on Campus: PolyU: Oct 2024 - Oct 2025, UI/UX Associate (Figma)
     </p>
  </div>

  <div v-else-if="pageStatus === 2" key="2">
    <p class="industry">
      Google Developer Group (GDG) on Campus: PolyU: Nov 2025 - Present, Graphic Designer Associate (Figma)
    </p>
    <p class="industry1">
      
    </p>
  </div>
</Transition>
  <div class="pagination corner1">
          <button @click="prevStatus" :disabled="pageStatus === 1">Prev</button>
          <button @click="nextStatus" :disabled="pageStatus === totalStatus">Next</button>
        </div>
      </div>

    </div>
  </div>
  
  </Transition>
  <div class="main2">
<div class="grid1">
 <div class="skills" :class="{ show: skillsVisible }">
  
  <div class="skills-grid">
  <div class="skill-box">
    <i class="fa-brands fa-figma"></i>
    <span>Figma</span>
  </div>

  <div class="skill-box">
   <span class="iconify" data-icon="simple-icons:adobexd"></span>
    <span>Adobe XD</span>
  </div>

  <div class="skill-box">
    <i class="fa-brands fa-js"></i>
    <span>JavaScript</span>
  </div>

  <div class="skill-box">
    <i class="fa-brands fa-vuejs"></i>
    <span>Vue</span>
  </div>

  <div class="skill-box">
    <i class="fa-brands fa-react"></i>
    <span>React</span>
  </div>

  <div class="skill-box">
    <i class="fa-brands fa-php"></i>
    <span>PHP</span>
  </div>

  <div class="skill-box">
    <i class="fa-brands fa-laravel"></i>
    <span>Laravel</span>
  </div>

  <div class="skill-box">
    <i class="fa-solid fa-database"></i>
    <span>Firebase</span>
  </div>
</div>
</div>
<div class="skills2">
 <h1>Skills</h1>
   </div>
   
      
 <Transition :name="slideTransition" mode="out-in">
  <div
    :key="activeSlide"
    class="card5"
    ref="cardRef"
    
  >
  <img
    :src="activeBackground"
    alt="Slide Image"
    class="card5-img"
  />
    <!-- card-inner wraps all content -->
    
      <!-- any content inside the card -->
       
   <div class="paginationcorner2">
  <!-- pagination buttons -->
  <button
    v-for="n in totalSlides"
    :key="n"
    @click="activeSlide = n; restartSlideshow()"
    :class="{ active: activeSlide === n }"
  ></button>
</div>

<!-- Conditional View button (separate div for rectangle) -->
<a
  v-if="activeSlide === 1"
  href="https://yellow-card-five.vercel.app/"
  target="_blank"
  class="view-btn1"
>
  View
</a>

<a
  v-if="activeSlide === 2"
  href="https://sparkfest-2025.vercel.app/"
  target="_blank"
  class="view-btn"
>
  View
</a>

<a
  v-if="activeSlide === 5"
  href="https://drive.google.com/drive/folders/1wZB-VUX0RovH0PgMw94oNVEClxXh78TH?usp=sharing"
  target="_blank"
  class="view-btn2"
>
  View
</a>

  </div>
</Transition>



   <div class ="card6">
   <h1>Highlighted Works</h1>

   </div>
   </div>
   </div>
   

</template>


<style scoped src="@/assets/profile.css"></style>


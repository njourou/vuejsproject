<template>
  <div>
    <!-- Header -->
    <header id="header" class="header d-flex align-items-center fixed-top">
      <div class="container-fluid container-xl position-relative d-flex align-items-center justify-content-between">
        <router-link to="/" class="logo d-flex align-items-center">
          <h1 class="sitename">TIKITI ZOTE</h1>
        </router-link>

        <nav id="navmenu" class="navmenu">
          <ul>
            <li><router-link to="/" class="active">Home</router-link></li>
            <li><a href="#tickets">Tickets</a></li>
            <li><a href="#contact">Contact</a></li>
            <li><router-link to="/admin/login" class="btn-login">Login</router-link></li>
          </ul>
          <i class="mobile-nav-toggle d-xl-none bi bi-list"></i>
        </nav>
      </div>
    </header>

    <!-- Hero Section -->
    <main class="main">
      <section id="hero" class="hero section dark-background">
        <div class="container text-center" data-aos="fade-up">
          <div class="row justify-content-center">
            <div class="col-lg-8">
              <h2>Welcome to TIKITI ZOTE</h2>
           
              <router-link to="#tickets" class="btn-get-started">Get Tickets</router-link>
            </div>
          </div>
        </div>
      </section>

      <!-- Portfolio Section -->
      <section id="tickets" class="portfolio section">
        <div class="container section-title" data-aos="fade-up">
          <h2>Available Tickets</h2>
          <p>Check out amazing destinations!</p>
        </div>

        <div class="container">
          <div class="row">
            <!-- Loop through the tours and display them dynamically -->
            <div
              v-for="tour in tours"
              :key="tour.id"
              class="col-lg-3 col-md-6 portfolio-item"
            >
              <div class="portfolio-content">
                <img :src="tour.image" class="img-fluid" alt="Tour Image">
                <div class="portfolio-info">
                  <h4>{{ tour.name }}</h4>
                  <p>{{ tour.description }}</p>
                  <p>Price: {{ tour.price }}</p>
                  <p>Slots: {{ tour.slots }}</p>
                  <p>Date: {{ tour.date }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
    </main>

    <!-- Scroll Top Button -->
    <a href="#" id="scroll-top" class="scroll-top d-flex align-items-center justify-content-center">
      <i class="bi bi-arrow-up-short"></i>
    </a>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'LandingPage',
  data() {
    return {
      tours: [], // Store tours data here
    };
  },
  methods: {
    // Fetch tours from the API
    fetchTours() {
      axios
        .get('http://127.0.0.1:8000/api/tours')
        .then((response) => {
          this.tours = response.data;
        })
        .catch((error) => {
          console.error('Error fetching tours:', error);
        });
    },
    resetNewTour() {
      this.newTour = {
        destination_id: '',
        name: '',
        description: '',
        price: '',
        slots: '',
        date: '',
        image: null,
      };
    },
  },
  mounted() {
    // Fetch tours when the component is mounted
    this.fetchTours();
  },
};
</script>

<style scoped>
.portfolio-item {
  margin-bottom: 30px;
}
.portfolio-content {
  position: relative;
  overflow: hidden;
}
.portfolio-info {
  margin-top: 10px;
  text-align: center;
}
</style>

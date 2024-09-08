<template>
    <div>
      <AdminHeader />
      <AdminSidebar />
  
      <main id="main" class="main">
        <div class="pagetitle">
          <h1>Manage Bookings</h1>
          <nav>
            <ol class="breadcrumb">
              <li class="breadcrumb-item"><a href="index.html">Home</a></li>
              <li class="breadcrumb-item active">Manage Bookings</li>
            </ol>
          </nav>
        </div>
  
        <section class="section dashboard">
          <div class="row">
            <div class="col-12 d-flex justify-content-between align-items-center mb-3">
              <h2>Booking Status</h2>
            </div>
  
            <!-- Booking Tiles -->
            <div class="col-12">
              <div class="row">
                <div class="col-md-4 mb-3">
                  <div class="tile tile-approved">
                    <h3>Approved Bookings</h3>
                    <p>{{ approvedCount }}</p>
                  </div>
                </div>
                <div class="col-md-4 mb-3">
                  <div class="tile tile-pending">
                    <h3>Pending Bookings</h3>
                    <p>{{ pendingCount }}</p>
                  </div>
                </div>
                <div class="col-md-4 mb-3">
                  <div class="tile tile-incomplete">
                    <h3>Incomplete Bookings</h3>
                    <p>{{ incompleteCount }}</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>
      </main>
    </div>
  </template>
  
  <script>
  import AdminHeader from '@/components/AdminLayout/AdminHeader.vue';
  import AdminSidebar from '@/components/AdminLayout/AdminSidebar.vue';
  import axios from 'axios';
  
  export default {
    components: {
      AdminHeader,
      AdminSidebar,
    },
    data() {
      return {
        approvedCount: 0,
        pendingCount: 0,
        incompleteCount: 0,
      };
    },
    async created() {
      try {
        // Fetch booking data (replace with your API endpoint)
        const response = await axios.get('http://127.0.0.1:8000/api/bookings/status');
        const { approved, pending, incomplete } = response.data;
  
        this.approvedCount = approved;
        this.pendingCount = pending;
        this.incompleteCount = incomplete;
      } catch (error) {
        console.error('Error fetching booking status:', error);
      }
    },
  };
  </script>
  
  <style scoped>
  .tile {
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(10px);
    border-radius: 15px;
    color: #fff;
    padding: 20px;
    text-align: center;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  }
  
  .tile h3 {
    margin: 0;
    font-size: 1.5rem;
  }
  
  .tile p {
    font-size: 2rem;
    margin: 0;
    font-weight: bold;
  }
  
  .tile-approved {
    background-color: #4CAF50;
  }
  
  .tile-pending {
    background-color: #FFC107;
  }
  
  .tile-incomplete {
    background-color: #DC3545;
  }
  </style>
  
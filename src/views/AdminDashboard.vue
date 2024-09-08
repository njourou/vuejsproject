<template>
  <div>
    <AdminHeader />
    <AdminSidebar />

    <main id="main" class="main">
      <div class="pagetitle">
        <h1>Dashboard</h1>
        <nav>
          <ol class="breadcrumb">
            <li class="breadcrumb-item"><a href="index.html">Home</a></li>
            <li class="breadcrumb-item active">Dashboard</li>
          </ol>
        </nav>
      </div>

      <section class="section dashboard">
        <div class="row">

     
          <div class="col-md-4 mb-3">
            <div class="card info-card sales-card glass-effect">

              <div class="filter">
                <a class="icon" href="#" data-bs-toggle="dropdown"><i class="fas fa-ellipsis-h"></i></a>
                <ul class="dropdown-menu dropdown-menu-end dropdown-menu-arrow">
                  <li class="dropdown-header text-start">
                    <h6>Filter</h6>
                  </li>

                  <li><a class="dropdown-item" href="#">Today</a></li>
                  <li><a class="dropdown-item" href="#">This Month</a></li>
                  <li><a class="dropdown-item" href="#">This Year</a></li>
                </ul>
              </div>

              <div class="card-body">
                <h5 class="card-title">Sales <span>| Today</span></h5>

                <div class="d-flex align-items-center">
                  <div class="card-icon rounded-circle d-flex align-items-center justify-content-center">
                    <i class="fas fa-shopping-cart"></i>
                  </div>
                  <div class="ps-3">
                    <h6>145</h6>
                    <span class="text-success small pt-1 fw-bold">12%</span> <span class="text-muted small pt-2 ps-1">increase</span>
                  </div>
                </div>
              </div>

            </div>
          </div><!-- End Sales Card -->

          <!-- Revenue Card -->
          <div class="col-md-4 mb-3">
            <div class="card info-card revenue-card glass-effect">

              <div class="filter">
                <a class="icon" href="#" data-bs-toggle="dropdown"><i class="fas fa-ellipsis-h"></i></a>
                <ul class="dropdown-menu dropdown-menu-end dropdown-menu-arrow">
                  <li class="dropdown-header text-start">
                    <h6>Filter</h6>
                  </li>

                  <li><a class="dropdown-item" href="#">Today</a></li>
                  <li><a class="dropdown-item" href="#">This Month</a></li>
                  <li><a class="dropdown-item" href="#">This Year</a></li>
                </ul>
              </div>

              <div class="card-body">
                <h5 class="card-title">Revenue <span>| This Month</span></h5>

                <div class="d-flex align-items-center">
                  <div class="card-icon rounded-circle d-flex align-items-center justify-content-center">
                    <i class="fas fa-dollar-sign"></i>
                  </div>
                  <div class="ps-3">
                    <h6>$3,264</h6>
                    <span class="text-success small pt-1 fw-bold">8%</span> <span class="text-muted small pt-2 ps-1">increase</span>
                  </div>
                </div>
              </div>

            </div>
          </div><!-- End Revenue Card -->

          <!-- Events Card -->
          <div class="col-md-4 mb-3">
            <div class="card info-card events-card glass-effect">

              <div class="filter">
                <a class="icon" href="#" data-bs-toggle="dropdown"><i class="fas fa-ellipsis-h"></i></a>
                <ul class="dropdown-menu dropdown-menu-end dropdown-menu-arrow">
                  <li class="dropdown-header text-start">
                    <h6>Filter</h6>
                  </li>

                  <li><a class="dropdown-item" href="#">Today</a></li>
                  <li><a class="dropdown-item" href="#">This Month</a></li>
                  <li><a class="dropdown-item" href="#">This Year</a></li>
                </ul>
              </div>

              <div class="card-body">
                <h5 class="card-title">Events <span>| This Month</span></h5>

                <div class="d-flex align-items-center">
                  <div class="card-icon rounded-circle d-flex align-items-center justify-content-center">
                    <i class="fas fa-calendar-alt"></i>
                  </div>
                  <div class="ps-3">
                    <h6>12</h6>
                    <span class="text-success small pt-1 fw-bold">5%</span> <span class="text-muted small pt-2 ps-1">increase</span>
                  </div>
                </div>
              </div>

            </div>
          </div><!-- End Events Card -->

        </div>
      </section>
    </main><!-- End #main -->
  </div>
</template>

<script>
import AdminHeader from '@/components/AdminLayout/AdminHeader.vue';
import AdminSidebar from '@/components/AdminLayout/AdminSidebar.vue';

export default {
  components: {
    AdminHeader,
    AdminSidebar,
  },
};
</script>

<style scoped>
.card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border-radius: 15px;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.card-body {
  padding: 1.5rem;
}

.card-icon {
  background: rgba(255, 255, 255, 0.3);
  color: #fff;
}

.info-card {
  border: none;
  color: #fff;
}

.sales-card {
  background: linear-gradient(135deg, #f3a683, #f7d794);
}

.revenue-card {
  background: linear-gradient(135deg, #f8c291, #e77f8d);
}

.events-card {
  background: linear-gradient(135deg, #80ed99, #1e272e);
}

.col-md-4 {
  padding: 0 1rem;
}

.mb-3 {
  margin-bottom: 1.5rem;
}
</style>

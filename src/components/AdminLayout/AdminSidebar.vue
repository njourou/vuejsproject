<template>
  <aside id="sidebar" class="sidebar">
    <ul class="sidebar-nav" id="sidebar-nav">

      <!-- Dashboard -->
      <li class="nav-item">
        <router-link to="/admin" class="nav-link">
          <i class="fas fa-home"></i> <!-- FontAwesome icon -->
          <span>Dashboard</span>
        </router-link>
      </li>

      <!-- Users Management -->
      <li class="nav-item">
        <a class="nav-link collapsed" data-bs-target="#users-nav" data-bs-toggle="collapse" href="#">
          <i class="fas fa-users"></i> <!-- FontAwesome icon -->
          <span>Users</span>
          <i class="fas fa-chevron-down ms-auto"></i>
        </a>
        <ul id="users-nav" class="nav-content collapse" data-bs-parent="#sidebar-nav">
          <li>
            <router-link to="/admin/users">
              <i class="fas fa-user-cog"></i>
              <span>Manage Users</span>
            </router-link>
          </li>
        </ul>
      </li>

      <!-- Tours Management -->
      <!-- Tours Management -->
<li class="nav-item">
  <a class="nav-link collapsed" data-bs-target="#tours-nav" data-bs-toggle="collapse" href="#">
    <i class="fas fa-map-signs"></i> <!-- FontAwesome icon -->
    <span>Tours</span>
    <i class="fas fa-chevron-down ms-auto"></i>
  </a>
  <ul id="tours-nav" class="nav-content collapse" data-bs-parent="#sidebar-nav">
    <li>
      <router-link to="/admin/tours">
        <i class="fas fa-route"></i>
        <span>Manage Tours</span>
      </router-link>
    </li>
  </ul>
</li>

      <!-- Destinations Management -->
      <li class="nav-item">
        <a class="nav-link collapsed" data-bs-target="#destinations-nav" data-bs-toggle="collapse" href="#">
          <i class="fas fa-map-marker-alt"></i> <!-- FontAwesome icon -->
          <span>Destinations</span>
          <i class="fas fa-chevron-down ms-auto"></i>
        </a>
        <ul id="destinations-nav" class="nav-content collapse" data-bs-parent="#sidebar-nav">
          <li>
            <router-link to="/admin/destinations">
              <i class="fas fa-globe"></i>
              <span>Manage Destinations</span>
            </router-link>
          </li>
        </ul>
      </li>

      <!-- Bookings Management -->
      <li class="nav-item">
        <a class="nav-link collapsed" data-bs-target="#bookings-nav" data-bs-toggle="collapse" href="#">
          <i class="fas fa-book"></i> <!-- FontAwesome icon -->
          <span>Bookings</span>
          <i class="fas fa-chevron-down ms-auto"></i>
        </a>
        <ul id="bookings-nav" class="nav-content collapse" data-bs-parent="#sidebar-nav">
          <li>
            <router-link to="/admin/bookings">
              <i class="fas fa-calendar-check"></i>
              <span>Manage Bookings</span>
            </router-link>
          </li>
        </ul>
      </li>

      <!-- Tickets Management -->
      <li class="nav-item">
        <a class="nav-link collapsed" data-bs-target="#tickets-nav" data-bs-toggle="collapse" href="#">
          <i class="fas fa-ticket-alt"></i> <!-- FontAwesome icon -->
          <span>Tickets</span>
          <i class="fas fa-chevron-down ms-auto"></i>
        </a>
        <ul id="tickets-nav" class="nav-content collapse" data-bs-parent="#sidebar-nav">
          <li>
            <router-link to="/admin/tickets">
              <i class="fas fa-list"></i>
              <span>View Tickets</span>
            </router-link>
          </li>
        </ul>
      </li>

      <!-- Reports -->
      <li class="nav-item">
        <a class="nav-link collapsed" data-bs-target="#reports-nav" data-bs-toggle="collapse" href="#">
          <i class="fas fa-chart-bar"></i> <!-- FontAwesome icon -->
          <span>Reports</span>
          <i class="fas fa-chevron-down ms-auto"></i>
        </a>
        <ul id="reports-nav" class="nav-content collapse" data-bs-parent="#sidebar-nav">
          <li>
            <router-link to="/admin/tour-reports">
              <i class="fas fa-file-alt"></i>
              <span>Tour Reports</span>
            </router-link>
          </li>
          <li>
            <router-link to="/admin/booking-reports">
              <i class="fas fa-file-invoice"></i>
              <span>Booking Reports</span>
            </router-link>
          </li>
        </ul>
      </li>

      <!-- Settings -->
      <li class="nav-item">
        <a class="nav-link collapsed" data-bs-target="#settings-nav" data-bs-toggle="collapse" href="#">
          <i class="fas fa-cog"></i> <!-- FontAwesome icon -->
          <span>Settings</span>
          <i class="fas fa-chevron-down ms-auto"></i>
        </a>
        <ul id="settings-nav" class="nav-content collapse" data-bs-parent="#sidebar-nav">
          <li>
            <router-link to="/admin/app-settings">
              <i class="fas fa-wrench"></i>
              <span>App Settings</span>
            </router-link>
          </li>
          <li>
            <router-link to="/admin/notifications">
              <i class="fas fa-bell"></i>
              <span>Notifications</span>
            </router-link>
          </li>
        </ul>
      </li>

      <!-- Logout -->
      <li class="nav-item">
        <router-link to="/admin/logout" class="nav-link">
          <i class="fas fa-sign-out-alt"></i> <!-- FontAwesome icon -->
          <span>Logout</span>
        </router-link>
      </li>

    </ul>
  </aside>
</template>

<script>
export default {
  name: "AdminSidebar",
};
</script>

<style scoped>
/* Add any custom styles if necessary */
</style>

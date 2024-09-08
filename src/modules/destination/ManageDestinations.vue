<template>
  <div>
    <AdminHeader />
    <AdminSidebar />

    <main id="main" class="main">
      <div class="pagetitle">
        <h1>Manage Destinations</h1>
        <nav>
          <ol class="breadcrumb">
            <li class="breadcrumb-item"><a href="index.html">Home</a></li>
            <li class="breadcrumb-item active">Manage Destinations</li>
          </ol>
        </nav>
      </div>

      <section class="section dashboard">
        <div class="row">
          <div class="col-12 d-flex justify-content-between align-items-center mb-3">
            <h2>Destinations</h2>
            <button class="btn btn-primary" @click="addDestination">Add Destination</button>
          </div>

          <!-- Destinations Table -->
          <div class="col-12">
            <table class="table table-striped table-hover">
              <thead>
                <tr>
                  <th scope="col">Name</th>
                  <th scope="col">Slug</th>
                  <th scope="col">Description</th>
                  <th scope="col">Date</th>
                  <th scope="col">Actions</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="destination in destinations" :key="destination.id">
                  <td>{{ destination.name }}</td>
                  <td>{{ destination.slug }}</td>
                  <td>{{ destination.description }}</td>
                  <td>{{ formatDate(destination.date) }}</td>
                  <td>
                    <button class="btn btn-warning btn-sm" @click="editDestination(destination)">Edit</button>
                    <button class="btn btn-danger btn-sm" @click="deleteDestination(destination.id)">Delete</button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
import AdminHeader from '@/components/AdminLayout/AdminHeader.vue';
import AdminSidebar from '@/components/AdminLayout/AdminSidebar.vue';
import Swal from 'sweetalert2';
import axios from 'axios';

export default {
  components: {
    AdminHeader,
    AdminSidebar,
  },
  data() {
    return {
      destinations: [],
    };
  },
  created() {
    this.fetchDestinations();
  },
  methods: {
    async fetchDestinations() {
      try {
        const response = await axios.get('http://127.0.0.1:8000/api/destinations');
        this.destinations = response.data;
      } catch (error) {
        console.error('Error fetching destinations:', error);
      }
    },
    async addDestination() {
      const { value: formValues } = await Swal.fire({
        title: 'Add New Destination',
        html: `
          <input id="swal-input1" class="swal2-input" placeholder="Name">
          <input id="swal-input2" class="swal2-input" placeholder="Slug">
          <textarea id="swal-input3" class="swal2-textarea" placeholder="Description"></textarea>
          <input id="swal-input4" class="swal2-input" type="date" placeholder="Date">
        `,
        focusConfirm: false,
        preConfirm: () => {
          const name = document.getElementById('swal-input1').value;
          const slug = document.getElementById('swal-input2').value;
          const description = document.getElementById('swal-input3').value;
          const date = document.getElementById('swal-input4').value;

          if (!name || !slug || !description || !date) {
            Swal.showValidationMessage('Please fill in all fields');
            return false;
          }

          return { name, slug, description, date };
        },
        confirmButtonText: 'Add Destination',
      });

      if (formValues) {
        try {
          await axios.post('http://127.0.0.1:8000/api/destinations', formValues);
          this.fetchDestinations();
          Swal.fire('Success!', 'Destination added successfully.', 'success');
        } catch (error) {
          Swal.fire('Error!', 'Failed to add destination.', 'error');
        }
      }
    },
    async editDestination(destination) {
      const { value: formValues } = await Swal.fire({
        title: 'Edit Destination',
        html: `
          <input id="swal-input1" class="swal2-input" value="${destination.name}" placeholder="Name">
          <input id="swal-input2" class="swal2-input" value="${destination.slug}" placeholder="Slug">
          <textarea id="swal-input3" class="swal2-textarea" placeholder="Description">${destination.description}</textarea>
          <input id="swal-input4" class="swal2-input" type="date" value="${destination.date}" placeholder="Date">
        `,
        focusConfirm: false,
        preConfirm: () => {
          const name = document.getElementById('swal-input1').value;
          const slug = document.getElementById('swal-input2').value;
          const description = document.getElementById('swal-input3').value;
          const date = document.getElementById('swal-input4').value;

          if (!name || !slug || !description || !date) {
            Swal.showValidationMessage('Please fill in all fields');
            return false;
          }

          return { name, slug, description, date };
        },
        confirmButtonText: 'Save Changes',
      });

      if (formValues) {
        try {
          await axios.put(`http://127.0.0.1:8000/api/destinations/${destination.id}`, formValues);
          this.fetchDestinations();
          Swal.fire('Success!', 'Destination updated successfully.', 'success');
        } catch (error) {
          Swal.fire('Error!', 'Failed to update destination.', 'error');
        }
      }
    },
    async deleteDestination(destinationId) {
      const result = await Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to recover this destination!",
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, delete it!',
      });

      if (result.isConfirmed) {
        try {
          await axios.delete(`http://127.0.0.1:8000/api/destinations/${destinationId}`);
          this.fetchDestinations();
          Swal.fire('Deleted!', 'Destination has been deleted.', 'success');
        } catch (error) {
          Swal.fire('Error!', 'Failed to delete destination.', 'error');
        }
      }
    },
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' };
      return new Date(date).toLocaleDateString(undefined, options);
    },
  },
};
</script>

<style scoped>
.table {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border-radius: 15px;
  color: #fff;
}

thead th {
  background-color: rgba(0, 0, 0, 0.1);
  color: #fff;
}

.table-hover tbody tr:hover {
  background-color: rgba(255, 255, 255, 0.2);
}

.btn-primary {
  background-color: #4CAF50;
  border-color: #4CAF50;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
}

.btn-primary:hover {
  background-color: #45a049;
  border-color: #45a049;
}

.btn-warning {
  background-color: #FFC107;
  border-color: #FFC107;
  color: #000;
}

.btn-warning:hover {
  background-color: #e0a800;
  border-color: #e0a800;
}

.btn-danger {
  background-color: #DC3545;
  border-color: #DC3545;
  color: #fff;
}

.btn-danger:hover {
  background-color: #c82333;
  border-color: #bd2130;
}
</style>

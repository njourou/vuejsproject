<template>
  <div>
    <AdminHeader />
    <AdminSidebar />

    <main id="main" class="main">
      <div class="pagetitle">
        <h1>Manage Tours</h1>
        <nav>
          <ol class="breadcrumb">
            <li class="breadcrumb-item"><a href="index.html">Home</a></li>
            <li class="breadcrumb-item active">Manage Tours</li>
          </ol>
        </nav>
      </div>

      <section class="section dashboard">
        <div class="row">
          <div class="col-12 d-flex justify-content-between align-items-center mb-3">
            <h2>Tour List</h2>
            <button class="btn btn-primary" @click="showAddTourModal">Add Tour</button>
          </div>

          <!-- Tour Table -->
          <div class="col-12">
            <table class="table table-striped table-hover">
              <thead>
                <tr>
                  <th scope="col">Image</th>
                  <th scope="col">Destination</th>
                  <th scope="col">Name</th>
                  <th scope="col">Description</th>
                  <th scope="col">Price</th>
                  <th scope="col">Slots</th>
                  <th scope="col">Date</th>
                  <th scope="col">Actions</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="tour in tours" :key="tour.id">
                  <td><img :src="`/storage/${tour.image}`" alt="Tour Image" width="100"></td>
                  <td>{{ tour.destination.name }}</td>
                  <td>{{ tour.name }}</td>
                  <td>{{ tour.description }}</td>
                  <td>{{ tour.price }}</td>
                  <td>{{ tour.slots }}</td>
                  <td>{{ tour.date }}</td>
                  <td>
                    <button class="btn btn-warning btn-sm" @click="editTour(tour.id)">Edit</button>
                    <button class="btn btn-danger btn-sm" @click="deleteTour(tour.id)">Delete</button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </section>

      <!-- Add Tour Modal -->
      <div v-if="showModal" class="modal">
        <div class="modal-content">
          <span class="close" @click="closeModal">&times;</span>
          <h2>Add New Tour</h2>
          <form @submit.prevent="submitTour">
            <div class="form-group">
              <label for="destination">Destination</label>
              <select v-model="newTour.destination_id" class="form-control" id="destination">
                <option value="" disabled selected>Select Destination</option>
                <option v-for="dest in destinations" :key="dest.id" :value="dest.id">{{ dest.name }}</option>
              </select>
            </div>
            <div class="form-group">
              <label for="name">Name</label>
              <input v-model="newTour.name" type="text" class="form-control" id="name" placeholder="Tour Name" required />
            </div>
            <div class="form-group">
              <label for="description">Description</label>
              <textarea v-model="newTour.description" class="form-control" id="description" placeholder="Tour Description" required></textarea>
            </div>
            <div class="form-group">
              <label for="price">Price</label>
              <input v-model="newTour.price" type="number" class="form-control" id="price" placeholder="Tour Price" required />
            </div>
            <div class="form-group">
              <label for="slots">Slots</label>
              <input v-model="newTour.slots" type="number" class="form-control" id="slots" placeholder="Available Slots" required />
            </div>
            <div class="form-group">
              <label for="date">Date</label>
              <input v-model="newTour.date" type="date" class="form-control" id="date" required />
            </div>
            <div class="form-group">
              <label for="image">Image</label>
              <input @change="handleImageUpload" type="file" class="form-control" id="image" accept="image/*" required />
            </div>
            <button type="submit" class="btn btn-primary">Add Tour</button>
          </form>
        </div>
      </div>
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
      tours: [],
      destinations: [],
      showModal: false,
      newTour: {
        destination_id: '',
        name: '',
        description: '',
        price: '',
        slots: '',
        date: '',
        image: null,
      },
    };
  },
  async created() {
    await this.fetchTours();
    await this.fetchDestinations();
  },
  methods: {
    async fetchTours() {
      try {
        const response = await axios.get('http://127.0.0.1:8000/api/tours');
        this.tours = response.data;
      } catch (error) {
        console.error('Error fetching tours:', error);
      }
    },
    async fetchDestinations() {
      try {
        const response = await axios.get('http://127.0.0.1:8000/api/destinations');
        this.destinations = response.data;
      } catch (error) {
        console.error('Error fetching destinations:', error);
      }
    },
    showAddTourModal() {
      this.showModal = true;
    },
    closeModal() {
      this.showModal = false;
    },
    handleImageUpload(event) {
      this.newTour.image = event.target.files[0];
    },
    async submitTour() {
      const formData = new FormData();
      formData.append('destination_id', this.newTour.destination_id);
      formData.append('name', this.newTour.name);
      formData.append('description', this.newTour.description);
      formData.append('price', this.newTour.price);
      formData.append('slots', this.newTour.slots);
      formData.append('date', this.newTour.date);
      formData.append('image', this.newTour.image);

      try {
        await axios.post('http://127.0.0.1:8000/api/tours', formData, {
          headers: {
            'Content-Type': 'multipart/form-data',
          },
        });
        this.closeModal();
        this.fetchTours();
        this.resetNewTour();
        alert('Tour added successfully');
      } catch (error) {
        console.error('Error adding tour:', error);
      }
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
    async editTour(tourId) {
      // Implement edit functionality
      console.log(`Edit tour with ID ${tourId}`);
    },
    async deleteTour(tourId) {
      if (confirm(`Are you sure you want to delete tour with ID ${tourId}?`)) {
        try {
          await axios.delete(`http://127.0.0.1:8000/api/tours/${tourId}`);
          this.fetchTours();
          alert('Tour deleted successfully');
        } catch (error) {
          console.error('Error deleting tour:', error);
        }
      }
    },
  },
};
</script>

<style scoped>
/* Basic styling for modal */
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-content {
  background: #fff;
  padding: 20px;
  border-radius: 8px;
  width: 500px;
}

.close {
  position: absolute;
  top: 10px;
  right: 20px;
  cursor: pointer;
  font-size: 24px;
  color: #000;
}

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
  color: white;
}

.btn-warning:hover {
  background-color: #ffb300;
  border-color: #ffb300;
}

.btn-danger {
  background-color: #f44336;
  border-color: #f44336;
  color: white;
}

.btn-danger:hover {
  background-color: #d32f2f;
  border-color: #d32f2f;
}
</style>

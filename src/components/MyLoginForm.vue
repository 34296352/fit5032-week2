<template>
  <div class="container mt-5">
    <h2 class="text-center mb-4">User Information Form</h2>
    <form @submit.prevent="submitForm">
      <div class="row row-cols-2">
        <div class="col mb-3">
          <label for="username" class="form-label">Username</label>
          <input type="text" class="form-control" id="username" v-model="formData.username" />
        </div>
        <div class="col mb-3">
          <label for="password" class="form-label">Password</label>
          <input type="password" class="form-control" id="password" v-model="formData.password" />
        </div>
        <div class="col mb-3">
          <div class="form-check mt-4">
            <input class="form-check-input" type="checkbox" id="resident" v-model="formData.isAustralian" />
            <label class="form-check-label" for="resident">Australian Resident?</label>
          </div>
        </div>
        <div class="col mb-3">
          <label for="gender" class="form-label">Gender</label>
          <select class="form-select" id="gender" v-model="formData.gender">
            <option disabled value="">Select gender</option>
            <option>Male</option>
            <option>Female</option>
            <option>Other</option>
          </select>
        </div>
        <div class="col-12 mb-3">
          <label for="reason" class="form-label">Reason for joining</label>
          <textarea class="form-control" id="reason" rows="3" v-model="formData.reason"></textarea>
        </div>
        <div class="col-12">
          <button type="submit" class="btn btn-primary me-2">Submit</button>
          <button type="reset" class="btn btn-secondary">Clear</button>
        </div>
      </div>
    </form>
  </div>
</template>


<script setup>
import { ref } from 'vue';

const formData = ref({
  username: '',
  password: '',
  isAustralian: false,
  reason: '',
  gender: ''
});

const submittedCards = ref([]);

const submitForm = () => {
  submittedCards.value.push({ ...formData.value });
};
</script>

<style scoped>
h1 {
  text-shadow: 4px 4px 8px rgba(0, 0, 0, 0.5);
}

.card {
  border: 1px solid #ccc;
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.card-header {
  background-color: #275FDA;
  color: white;
  padding: 10px;
  border-radius: 10px 10px 0 0;
}

.list-group-item {
  padding: 10px;
}
</style>

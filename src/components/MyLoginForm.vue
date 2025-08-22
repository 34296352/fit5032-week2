<template>
  <div class="container mt-5">
    <div class="row">
      <div class="col-md-10 offset-md-1">
        <h1 class="text-center mb-4">User Information Form</h1>
        <form @submit.prevent="submitForm">
          <div class="row">
            <!-- Username -->
            <div class="col-md-6 mb-3">
                <label for="username" class="form-label">Username</label>
                <input
                    type="text"
                    id="username"
                    v-model="formData.username"
                    class="form-control"
                    @blur="() => validateName(true)"
                    @input="() => validateName(false)"
                />
                <div v-if="errors.username" class="text-danger">{{ errors.username }}</div>
                </div>

            <!-- Password -->
            <div class="col-md-6 mb-3">
              <label for="password" class="form-label">Password</label>
              <input
                type="password"
                class="form-control"
                id="password"
                v-model="formData.password"
                @blur="() => validatePassword(true)"
                @input="() => validatePassword(false)"
                />
                <div v-if="errors.password" class="text-danger">{{ errors.password }}</div>


            </div>

            <!-- Australian Resident -->
            <div class="col-md-6 mb-3 d-flex align-items-center">
              <input type="checkbox" id="isAustralian" v-model="formData.isAustralian" class="form-check-input me-2"  />
              <label for="isAustralian" class="form-check-label mb-0">Australian Resident?</label>
            </div>

            <!-- Gender -->
            <div class="col-md-6 mb-3">
              <label for="gender" class="form-label">Gender</label>
              <select id="gender" v-model="formData.gender" class="form-select">
                <option value="female">Female</option>
                <option value="male">Male</option>
                <option value="other">Other</option>
              </select>
            </div>

            <!-- Reason For Joining -->
            <div class="col-12 mb-3">
              <label for="reason" class="form-label">Reason For Joining</label>
              <textarea id="reason" v-model="formData.reason" class="form-control" rows="3"></textarea>
            </div>

            <!-- Buttons -->
            <div class="col-12 text-center">
              <button type="submit" class="btn btn-primary me-2">Submit</button>
              <button type="reset" class="btn btn-secondary">Clear</button>
            </div>
          </div>
        </form>

        <!-- Display Cards -->
        <div class="row mt-5" v-if="submittedCards.length">
          <div class="d-flex flex-wrap justify-content-start">
            <div v-for="(card, index) in submittedCards" :key="index" class="card m-2" style="width: 18rem;">
              <div class="card-header">User Information</div>
              <ul class="list-group list-group-flush">
                <li class="list-group-item">Username: {{ card.username }}</li>
                <li class="list-group-item">Password: {{ card.password }}</li>
                <li class="list-group-item">Australian Resident: {{ card.isAustralian ? 'Yes' : 'No' }}</li>
                <li class="list-group-item">Gender: {{ card.gender }}</li>
                <li class="list-group-item">Reason: {{ card.reason }}</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
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

const errors = ref({
  username: null,
  password: null,
  resident: null,
  gender: null,
  reason: null,
});

const validateName = (blur) => {
  if (formData.value.username.length < 3) {
    if (blur) {
      errors.value.username = "Name must be at least 3 characters";
    }
  } else {
    errors.value.username = null;
  }
};
const submittedCards = ref([]);

const submitForm = () => {
  validateName(true);
  validatePassword(true);

  if (!errors.value.username && !errors.value.password) {
    submittedCards.value.push({ ...formData.value });
    clearForm();
  }
};

const validatePassword = (blur) => {
  const password = formData.value.password;
  const minLength = 8;
  const hasUppercase = /[A-Z]/.test(password);
  const hasLowercase = /[a-z]/.test(password);
  const hasNumber = /\d/.test(password);
  const hasSpecialChar = /[!@#$%^&*(),.?":{}|<>]/.test(password);

  if (password.length < minLength) {
    if (blur) errors.value.password = `Password must be at least ${minLength} characters long.`;
  } else if (!hasUppercase) {
    if (blur) errors.value.password = "Password must contain at least one uppercase letter.";
  } else if (!hasLowercase) {
    if (blur) errors.value.password = "Password must contain at least one lowercase letter.";
  } else if (!hasNumber) {
    if (blur) errors.value.password = "Password must contain at least one number.";
  } else if (!hasSpecialChar) {
    if (blur) errors.value.password = "Password must contain at least one special character.";
  } else {
    errors.value.password = null;
  }
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

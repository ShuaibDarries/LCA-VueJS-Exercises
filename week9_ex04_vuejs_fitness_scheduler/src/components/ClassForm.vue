<template>
  <section class="form-section">
    <h2>Add New Class Session</h2>
    <form @submit.prevent="handleSubmit" class="class-form">
      <div class="form-group">
        <label for="name">Class Name *</label>
        <input
          id="name"
          v-model="form.name"
          type="text"
          placeholder="e.g. Morning Yoga"
          :class="{ 'input-error': errors.name }"
        />
        <span v-if="errors.name" class="error-msg">{{ errors.name }}</span>
      </div>

      <div class="form-group">
        <label for="coach">Coach Name *</label>
        <input
          id="coach"
          v-model="form.coach"
          type="text"
          placeholder="e.g. Sarah Johnson"
          :class="{ 'input-error': errors.coach }"
        />
        <span v-if="errors.coach" class="error-msg">{{ errors.coach }}</span>
      </div>

      <div class="form-row">
        <div class="form-group">
          <label for="date">Date *</label>
          <input
            id="date"
            v-model="form.date"
            type="date"
            :class="{ 'input-error': errors.date }"
          />
          <span v-if="errors.date" class="error-msg">{{ errors.date }}</span>
        </div>

        <div class="form-group">
          <label for="time">Time *</label>
          <input
            id="time"
            v-model="form.time"
            type="time"
            :class="{ 'input-error': errors.time }"
          />
          <span v-if="errors.time" class="error-msg">{{ errors.time }}</span>
        </div>
      </div>

      <div class="form-group">
        <label for="capacity">Capacity *</label>
        <input
          id="capacity"
          v-model="form.capacity"
          type="number"
          min="1"
          placeholder="e.g. 20"
          :class="{ 'input-error': errors.capacity }"
        />
        <span v-if="errors.capacity" class="error-msg">{{ errors.capacity }}</span>
      </div>

      <button type="submit" class="submit-btn">Add Class Session</button>
    </form>
  </section>
</template>

<script>
import { reactive } from 'vue'

export default {
  name: 'ClassForm',
  emits: ['add-class'],
  setup(props, { emit }) {
    // Reactive form object using v-model
    const form = reactive({
      name: '',
      coach: '',
      date: '',
      time: '',
      capacity: ''
    })

    // Reactive errors object
    const errors = reactive({
      name: '',
      coach: '',
      date: '',
      time: '',
      capacity: ''
    })

    // Validation function
    const validate = () => {
      let isValid = true

      // Reset errors
      errors.name = ''
      errors.coach = ''
      errors.date = ''
      errors.time = ''
      errors.capacity = ''

      if (!form.name.trim()) {
        errors.name = 'Class name is required'
        isValid = false
      }

      if (!form.coach.trim()) {
        errors.coach = 'Coach name is required'
        isValid = false
      }

      if (!form.date) {
        errors.date = 'Date is required'
        isValid = false
      }

      if (!form.time) {
        errors.time = 'Time is required'
        isValid = false
      }

      if (!form.capacity || form.capacity < 1) {
        errors.capacity = 'Capacity must be at least 1'
        isValid = false
      }

      return isValid
    }

    // Handle form submission
    const handleSubmit = () => {
      if (validate()) {
        emit('add-class', {
          name: form.name.trim(),
          coach: form.coach.trim(),
          date: form.date,
          time: form.time,
          capacity: parseInt(form.capacity)
        })

        // Reset form
        form.name = ''
        form.coach = ''
        form.date = ''
        form.time = ''
        form.capacity = ''
      }
    }

    return {
      form,
      errors,
      handleSubmit
    }
  }
}
</script>

<style scoped>
.form-section {
  background: white;
  padding: 24px;
  border-radius: 12px;
  box-shadow: 0 2px 12px rgba(0,0,0,0.08);
  margin-bottom: 24px;
}

.form-section h2 {
  margin-bottom: 20px;
  color: #333;
  font-size: 1.3rem;
}

.class-form {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.form-group label {
  font-weight: 600;
  color: #555;
  font-size: 0.95rem;
}

.form-group input {
  padding: 12px 14px;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  font-size: 1rem;
  transition: border-color 0.3s, box-shadow 0.3s;
}

.form-group input:focus {
  outline: none;
  border-color: #667eea;
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.15);
}

.input-error {
  border-color: #e74c3c !important;
}

.error-msg {
  color: #e74c3c;
  font-size: 0.85rem;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
}

.submit-btn {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  padding: 14px 24px;
  border-radius: 8px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
  margin-top: 8px;
}

.submit-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(102, 126, 234, 0.35);
}

.submit-btn:active {
  transform: translateY(0);
}

@media (max-width: 600px) {
  .form-row {
    grid-template-columns: 1fr;
  }
}
</style>

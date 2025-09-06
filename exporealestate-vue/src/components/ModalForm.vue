<template>
  <div class="modal-overlay" @click="$emit('close')">
    <div class="modal-content" @click.stop>
      <button class="modal-close" @click="$emit('close')">
        <svg width="24" height="24" viewBox="0 0 24 24">
          <path d="M18 6L6 18M6 6L18 18" stroke="currentColor" stroke-width="2"/>
        </svg>
      </button>
      
      <div class="modal-header">
        <h2>Спасибо что выбрали нас!</h2>
        <p>Заполните форму и мы свяжемся с Вами, хорошего дня.</p>
        <div class="modal-logo">
          EXPO REAL ESTATE 2025: Международная выставка недвижимости в Москве
        </div>
      </div>
      
      <form @submit.prevent="submitForm" class="modal-form">
        <div class="form-group">
          <input 
            v-model="form.name"
            type="text" 
            placeholder="Ваше имя" 
            required
            class="form-input"
          />
        </div>
        
        <div class="form-group">
          <input 
            v-model="form.phone"
            type="tel" 
            placeholder="+7(999)-999-00-00" 
            required
            class="form-input"
          />
        </div>
        
        <div class="form-group">
          <textarea 
            v-model="form.message"
            placeholder="Сообщение" 
            rows="3"
            class="form-textarea"
          ></textarea>
        </div>
        
        <div class="form-group">
          <input 
            v-model="form.email"
            type="email" 
            placeholder="Ваш e-mail" 
            required
            class="form-input"
          />
        </div>
        
        <div class="form-group">
          <input 
            v-model="form.organization"
            type="text" 
            placeholder="Название организации" 
            class="form-input"
          />
        </div>
        
        <div class="form-group">
          <textarea 
            v-model="form.comment"
            placeholder="Комментарий" 
            rows="3"
            class="form-textarea"
          ></textarea>
        </div>
        
        <div class="form-checkbox">
          <label>
            <input 
              v-model="form.agreement"
              type="checkbox" 
              required
            />
            <span class="checkmark"></span>
            Я согласен на обработку персональных данных.
          </label>
        </div>
        
        <button type="submit" class="btn btn-large" :disabled="!form.agreement">
          Отправить
        </button>
      </form>
    </div>
  </div>
</template>

<script>
import { reactive } from 'vue'

export default {
  name: 'ModalForm',
  emits: ['close'],
  setup(props, { emit }) {
    const form = reactive({
      name: '',
      phone: '',
      email: '',
      organization: '',
      message: '',
      comment: '',
      agreement: false
    })
    
    const submitForm = () => {
      console.log('Modal form submitted:', form)
      alert('Спасибо! Ваше сообщение отправлено.')
      
      // Очистка формы и закрытие модального окна
      Object.keys(form).forEach(key => {
        if (key === 'agreement') {
          form[key] = false
        } else {
          form[key] = ''
        }
      })
      
      emit('close')
    }
    
    return {
      form,
      submitForm
    }
  }
}
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10000;
  padding: 2rem;
  backdrop-filter: blur(5px);
}

.modal-content {
  background: white;
  border-radius: 20px;
  max-width: 500px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
  animation: modalSlideIn 0.3s ease-out;
}

@keyframes modalSlideIn {
  from {
    opacity: 0;
    transform: translateY(-30px) scale(0.95);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.modal-close {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: rgba(216, 4, 42, 0.1);
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color-primary);
  cursor: pointer;
  transition: var(--transition);
  z-index: 1;
}

.modal-close:hover {
  background: var(--color-primary);
  color: white;
  transform: rotate(90deg);
}

.modal-header {
  padding: 2rem 2rem 1rem 2rem;
  text-align: center;
}

.modal-header h2 {
  color: var(--color-primary);
  font-size: 1.8rem;
  margin-bottom: 0.5rem;
}

.modal-header p {
  color: var(--color-secondary);
  margin-bottom: 1rem;
}

.modal-logo {
  background: linear-gradient(135deg, var(--color-primary), var(--color-accent));
  color: white;
  padding: 1rem;
  border-radius: 10px;
  font-size: 0.9rem;
  font-weight: var(--font-weight-medium);
  line-height: 1.3;
}

.modal-form {
  padding: 0 2rem 2rem 2rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-input,
.form-textarea {
  padding: 1rem 1.5rem;
  border: 2px solid rgba(216, 4, 42, 0.2);
  border-radius: 12px;
  font-size: 1rem;
  font-family: var(--font-primary);
  transition: var(--transition);
  background: rgba(237, 242, 245, 0.3);
}

.form-input:focus,
.form-textarea:focus {
  outline: none;
  border-color: var(--color-primary);
  box-shadow: 0 0 0 3px rgba(216, 4, 42, 0.1);
  background: white;
}

.form-textarea {
  resize: vertical;
  min-height: 80px;
}

.form-checkbox {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin: 0.5rem 0;
}

.form-checkbox label {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: pointer;
  font-size: 0.9rem;
  color: var(--color-secondary);
  line-height: 1.4;
}

.form-checkbox input[type="checkbox"] {
  opacity: 0;
  position: absolute;
}

.checkmark {
  width: 18px;
  height: 18px;
  border: 2px solid var(--color-primary);
  border-radius: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: var(--transition);
  flex-shrink: 0;
}

.form-checkbox input[type="checkbox"]:checked + .checkmark {
  background: var(--color-primary);
}

.form-checkbox input[type="checkbox"]:checked + .checkmark::after {
  content: '✓';
  color: white;
  font-weight: bold;
  font-size: 12px;
}

.btn-large {
  padding: 1rem 2rem;
  font-size: 1rem;
  align-self: center;
  margin-top: 0.5rem;
}

.btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
  transform: none;
}

.btn:disabled:hover {
  transform: none;
  box-shadow: none;
}

@media (max-width: 768px) {
  .modal-overlay {
    padding: 1rem;
  }
  
  .modal-header {
    padding: 1.5rem 1.5rem 1rem 1.5rem;
  }
  
  .modal-form {
    padding: 0 1.5rem 1.5rem 1.5rem;
  }
  
  .modal-header h2 {
    font-size: 1.5rem;
  }
  
  .modal-logo {
    font-size: 0.8rem;
    padding: 0.8rem;
  }
}
</style>
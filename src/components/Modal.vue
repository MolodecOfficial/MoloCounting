<script setup>
import { ref } from 'vue';

const emit = defineEmits( [
  'add', 'close'
])

const organization = ref({
  name: '',
  director: '',
  phone: ''
});

const close = () => {
  emit('close');
};

const addOrganization = () => {
  emit('add', { ...organization.value });
};
</script>

<template>
  <div class="modal">
    <div class="modal-content">
      <header class="modal-header">Добавить организацию</header>
      <div class="modal-body">
        <div class="modal-inputs">
          <input v-model="organization.name" placeholder="Название организации">
          <input v-model="organization.director" placeholder="ФИО директора">
          <input v-model="organization.phone" placeholder="Номер телефона">
        </div>
      </div>
      <div class="modal-footer">
        <button @click="close">Закрыть</button>
        <button @click="addOrganization">OK</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}
.modal-content {
  border: 1px solid black;
  margin: 10px;
}
.modal-inputs {
  display: flex;
  flex-direction: column;
}
.modal-header {
  margin: 10px;
}
input {
  height: 30px;
  margin: 5px 10px;
  text-align: center;
}
button {
  width: 80px;
  height: 30px;
  background-color: transparent;
  border: 2px solid #c5c3c3;
}
button:hover {
  border: 1px solid #9d9d9d;
}
.modal-footer {
  display: flex;
  margin: 10px;
  justify-content: space-between;
}
header {
  display: flex;
  justify-content: center;
}
</style>
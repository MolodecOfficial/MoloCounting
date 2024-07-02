<script setup>
import { ref, computed } from 'vue';
import Modal from "./components/Modal.vue";

const organizations = ref([
  { id: 1, name: 'ООО Вектор', director: 'Иванов И.И.', phone: '+70001234567'},
  { id: 2, name: 'ИП Сидоров С.С.', director: 'Сидоров С.С.', phone: '+7000567899'},
]);
const addOrganization = (newOrganization) => {
  organizations.value.push({ id: organizations.value.length + 1, ...newOrganization });
  closeModal();
}

const search = ref('');
const isModalOpen = ref(false);

const openModal = () => {
  isModalOpen.value = true;
};

const removeOrganization = (index) => {
  organizations.value.splice(index, 1);
  closeModal();
  console.log(index)
}
const closeModal = () => {
  isModalOpen.value = false;
};

const sortBy = (key) => {
  organizations.value.sort((a, b) => a[key].localeCompare(b[key]));
};

const displayedOrganizations = computed(() => {
  return organizations.value.filter((org) =>
      org.director.toLowerCase().includes(search.value.toLowerCase())
  );
});
</script>

<template>
  <div>
    <header>Справочник организаций</header>
    <section>
      <input v-model="search" placeholder="Найти по ФИО">
      <button @click="openModal">Добавить</button>
    </section>
    <div class="container">
      <table>
        <thead>
        <tr class="container-header">
          <th @click="sortBy('name')">Название</th>
          <th class="container-director" @click="sortBy('director')">ФИО директора</th>
          <th>Номер телефона</th>
          <th class="delete"></th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="(organization, index) in displayedOrganizations" :key="organization.id">
          <td>{{ organization.name }}</td>
          <td>{{ organization.director }}</td>
          <td>{{ organization.phone }}</td>
          <td class="delete" @click="removeOrganization(index)">&#215;</td>
        </tr>
        </tbody>
      </table>
    </div>
    <Modal v-if="isModalOpen" @close="closeModal" @add="addOrganization" />
  </div>
</template>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}
.container-header {
  border: 1px solid #939393;
}
.container-director {
  cursor: pointer;
}
.delete {
  cursor: pointer;
  width: 50px;
}
th {
  align-items: center;
  display: flex;
  justify-content: center;
  width: 150px;
  height: 30px;
  border: 2px solid #939393;
}
td {
  border: 1px solid #939393;
  width: 150px;
  height: 40px;
  align-items: center;
  display: flex;
  justify-content: center;
}
table {
  width: 550px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}
thead {
  display: flex;
  gap: 50px;
  justify-content: space-around;
}
tr {
  display: flex;
  justify-content: center;
}
header {
  display: flex;
  justify-content: center;
  font-size: 30px;
  font-family: Poppins, sans-serif;
  margin-top: 20px;
}
input {
  height: 30px;
  width: 110px;
  border-radius: 5px;
  border: 1px solid #a89f9f;
  text-align: center;
}
input::placeholder {
  text-align: center;
}
section {
  display: flex;
  justify-content: center;
  gap: 240px;
  margin-top: 80px;
}
button {
  width: 100px;
  background-color: transparent;
  border: 2px solid #c5c3c3;
}
button:hover {
  border: 1px solid #9d9d9d;
}

</style>

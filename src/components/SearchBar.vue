<template>
  <div class="search-bar-container">
    <!-- Search Bar -->
    <div class="search-bar">
      <input 
        type="text" 
        v-model="searchText" 
        @focus="showClearIcon = true"
        @blur="showClearIcon = false" 
        placeholder="Search..."
        class="search-input"
      />
      <button class="clear-btn" v-if="showClearIcon" @click="clearSearchText">
        <font-awesome-icon :icon="['fas', 'times']" />
      </button>
      <button class="search-btn">
        <font-awesome-icon :icon="['fas', 'search']" />
      </button>
    </div>

    <!-- Dropdown Boxes -->
    <div class="dropdown-container">
      <div 
        class="dropdown-box" 
        v-for="(box, index) in dropdownBoxes" 
        :key="index" 
        @click="toggleDropdown(index)"
      >
        <div class="box-content">
          <font-awesome-icon :icon="box.icon" />
          <span>{{ box.label }}</span>
        </div>
        <font-awesome-icon 
          v-if="index < dropdownBoxes.length - 2" 
          :icon="['fas', 'caret-down']" 
        />
      </div>
    </div>

    <!-- Dropdown Modal for Each Box -->
    <div v-if="activeDropdown !== null" class="dropdown-overlay" @click="closeDropdown">
      <div class="dropdown-modal" @click.stop>
        <div class="modal-content">
          <h4>{{ dropdownBoxes[activeDropdown].label }} Options</h4>
          <ul>
            <li v-for="(option, optionIndex) in dropdownBoxes[activeDropdown].options" :key="optionIndex">{{ option }}</li>
          </ul>
          <button @click="closeDropdown">Close</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { library } from '@fortawesome/fontawesome-svg-core';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { faSearch, faTimes, faCaretDown, faSliders, faPencilAlt } from '@fortawesome/free-solid-svg-icons';

library.add(faSearch, faTimes, faCaretDown, faSliders, faPencilAlt);

const searchText = ref('');
const showClearIcon = ref(false);
const activeDropdown = ref(null);

// Dropdown Boxes
const dropdownBoxes = ref([
  { label: 'For Sale', icon: 'home', options: ['Option 1', 'Option 2'] },
  { label: 'Price', icon: 'dollar-sign', options: ['Option 1', 'Option 2'] },
  { label: 'Beds & Baths', icon: 'bath', options: ['Option 1', 'Option 2'] },
  { label: 'Property Type', icon: 'building', options: ['Option 1', 'Option 2'] },
  { label: 'Filter', icon: faSliders, options: ['Option 1', 'Option 2'] },
  { label: 'Saved', icon: faPencilAlt, options: ['Option 1', 'Option 2'] },
]);

const toggleDropdown = (index) => {
  activeDropdown.value = activeDropdown.value === index ? null : index;
};

const closeDropdown = () => {
  activeDropdown.value = null;
};

const clearSearchText = () => {
  searchText.value = '';
  showClearIcon.value = false;
};
</script>


<style scoped>
.search-bar-container {
  display: flex;
  flex-direction: row;
  width: 100%;
  padding: 16px 14px;
  justify-content: flex-start;
  align-items: baseline;
  box-shadow: 10px 3px 5px 0px #98989833;
  gap: 20px;
  transition: opacity 0.3s ease;
}

.search-bar-container.modal-open {
  opacity: 0.3;
}

.search-bar {
  display: flex;
  align-items: center;
  border-radius: 40px;
  border: 1px solid #ccc;
  padding: 5px;
  background: white;
  position: relative;
  width: 387px;
}

.search-input {
  border: none;
  outline: none;
  padding: 10px 40px 10px 15px;
  width: 100%;
  border-radius: 20px;
}

.clear-btn, .search-btn {
  border: none;
  background: transparent;
  cursor: pointer;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}

.clear-btn {
  right: 50px;
}

.search-btn {
  right: 10px;
  border-radius: 50%;
  background-color: #0B5AA5;
  color: white;
  padding: 10px;
}

.dropdown-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  margin-top: 10px;
  font-size: 14px;
}

.dropdown-box {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: white;
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 14px 16px;
  width: 121px;
  cursor: pointer;
  height: 19px;
  transition: background-color 0.3s;
}

.dropdown-box:last-child {
  border-radius: 35px;
  width: 85px;
  padding: 15px 6px 14px 20px;
}

.dropdown-box:nth-last-child(2) {
  border-radius: 8px;
  width: 85px;
  padding: 15px 6px 14px 20px;
}

.dropdown-box:hover {
  background-color: #f0f0f0;
}

.box-content {
  display: flex;
  align-items: center;
  gap: 15px;
}

.dropdown-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  z-index: 99999;
  display: flex;
  align-items: center;
  justify-content: center;
}

.dropdown-modal {
  background: white;
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  z-index: 1000;
  width: 350px;
}

.modal-content h4 {
  margin-bottom: 10px;
}

.modal-content ul {
  list-style: none;
  padding: 0;
}

.modal-content li {
  padding: 10px 0;
}

.modal-content button {
  margin-top: 10px;
  padding: 5px 10px;
}

@media (max-width: 768px) {
  .search-bar-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.search-bar {
        width: 90%;
}
}

</style>



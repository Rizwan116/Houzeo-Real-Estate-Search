<template>
  <nav class="navbar">
    <div class="nav-content">
      <!-- Hamburger Menu -->
      <div class="hamburger" @click="toggleMobileMenu">
        <font-awesome-icon :icon="isMobileMenuOpen ? ['fas', 'times'] : ['fas', 'bars']" />
      </div>

      <!-- Logo -->
      <div class="logo">
        <img src="../assets/logo.png" alt="Houzeo">
      </div>

      <!-- User Icon -->
      <div class="user-icon">
        <font-awesome-icon :icon="['fas', 'user']" />
      </div>

      <!-- Navigation Menu -->
      <ul :class="['nav-menu', { 'mobile-menu-open': isMobileMenuOpen }]">
        <li v-for="(item, index) in navItems" :key="index" class="nav-item" @click="toggleDropdown(index)">
          <span class="nav-link">
            {{ item }}
            <font-awesome-icon v-if="!isSpecialNavItem(item)" :icon="['fas', 'caret-down']" />
          </span>
          <ul v-if="!isSpecialNavItem(item)" :class="['dropdown-menu', { 'dropdown-open': activeDropdown === index }]">
            <li v-for="(option, optionIndex) in dropdownOptions" :key="optionIndex">
              {{ option }}
            </li>
          </ul>
        </li>
        <div class="contact-info">
          <div class="phone-number">
            <a href="tel:(844) 448-0110" alias="(844) 448-0110" style="text-decoration: none;color: #000;">(844) 448-0110</a>
          </div>
          <div class="time">(9am to 6pm CST, Mon-Sat)</div>
        </div>
        <button class="free-listing-button"><b>Start Free Listing</b></button>
      </ul>
    </div>
  </nav>
</template>

<script setup>
import { ref } from 'vue';
import { library } from '@fortawesome/fontawesome-svg-core';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { faBars, faCaretDown, faUser, faTimes } from '@fortawesome/free-solid-svg-icons';

library.add(faBars, faCaretDown, faUser, faTimes);

const isMobileMenuOpen = ref(false);
const activeDropdown = ref(null);

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value;
  // Close any open dropdown when closing mobile menu
  if (!isMobileMenuOpen.value) {
    activeDropdown.value = null;
  }
};

const toggleDropdown = (index) => {
  if (activeDropdown.value === index) {
    activeDropdown.value = null;
  } else {
    activeDropdown.value = index;
  }
};

const navItems = [
  'Product',
  'How Houzeo Works',
  'Reviews',
  'Buy',
  'Sell',
  'Pricing',
  'Resources',
  'Sign In',
];

const dropdownOptions = ['Option 1', 'Option 2'];

// Function to check if the item is a special navigation item
const isSpecialNavItem = (item) => {
  return ['How Houzeo Works', 'Reviews', 'Pricing', 'Sign In'].includes(item);
};
</script>

<script>
export default {
  components: {
    FontAwesomeIcon,
  },
};
</script>

<style scoped>
.navbar {
  background-color: white;
  color: black;
  /* border-bottom: 1px solid #ccc; */
  padding: 20px;
  position: relative;
  z-index: 1;
  display: flex;
  justify-content: center;
  box-shadow: 10px 3px 5px 0px #98989833;
}

.nav-content {
  width: 100%;
  /* max-width: 1200px; */
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: relative;
}

.hamburger {
  font-size: 1.8em;
  cursor: pointer;
  display: none;
}

.logo {
  font-size: 1.5em;
  font-weight: bold;
  flex: 1;
  text-align: left;
}

.user-icon {
  border: 2px solid black;
  border-radius: 50%;
  padding: 5px;
  background: white;
  cursor: pointer;
  display: none;
}

.nav-menu {
  list-style: none;
  display: flex;
  gap: 20px;
  align-items: center;
  flex: 4;
  justify-content: right;
  transition: all 0.3s ease-in-out;
  font-size: 14px;
}

.nav-item {
  position: relative;
  cursor: pointer;
}

.nav-link {
  display: flex;
  align-items: normal;
  gap: 10px;
}

.nav-item:hover .dropdown-menu {
  display: block;
}

.dropdown-menu {
  display: none;
  position: absolute;
  top: 100%;
  left: 0;
  background-color: white;
  border: 1px solid #ccc;
  list-style: none;
  padding: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: max-content;
  opacity: 0;
  transition: all 0.3s ease-in-out;
  transform: translateY(-10px);
}

.dropdown-open {
  display: block;
  opacity: 1;
  transform: translateY(0);
  z-index: 999;
}

.dropdown-menu li {
  padding: 5px 10px;
  cursor: pointer;
}

.contact-info {
  display: flex;
  flex-direction: column;
  text-align: left;
  /* margin-left: 40px; */
}

.phone-number {
  /* font-weight: bold; */
}

.time {
  font-size: 12px;
  color: #777;
}

.free-listing-button {
  background: linear-gradient(to right, #0E5293, #2876C1);
  color: white;
  border: none;
  border-radius: 8px;
  padding: 10px 15px;
  cursor: pointer;
  transition: 0.3s;
  width: 154px;
}

.free-listing-button:hover {
  background: linear-gradient(to right, #0056b3, #0099cc);
}

@media (max-width: 768px) {
  .hamburger {
    display: block;
    z-index: 2;
  }

  .logo {
    text-align: center;
  }

  .user-icon {
    margin-left: auto;
    display: block;
  }

  .nav-menu {
    display: none;
    flex-direction: column;
    position: fixed;
    top: 0;
    left: 0;
    width: 70%;
    height: 100%;
    background-color: white;
    z-index: 1;
    padding: 20px;
    border-right: 1px solid #ccc;
    box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);
  }

  .nav-menu.mobile-menu-open {
    display: flex;
    justify-content: flex-start;
    padding-top: 60px;
  }

  .nav-item {
    padding: 10px 0;
    border-bottom: 1px solid #ccc;
    width: 100%;
    text-align: left;
  }

  .logo {
    position: static;
    transform: none;
  }

  .contact-info {
    align-items: flex-start;
    width: 100%;
    text-align: center;
  }

  .free-listing-button {
    margin: 15px 0;
    width: calc(100% - 40px);
    padding: 15px 10px;
  }
}
</style>

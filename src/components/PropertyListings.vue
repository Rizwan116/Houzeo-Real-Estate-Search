<template>
  <div class="property-listings">
    <div class="header">
     <div class="header-titles">
      <h3>Austin, TX real estate & homes for sale</h3>
      
      <div class="header-container">
      
      <div class="header-left">
        <p class="home-count">100 homes</p>
      </div>

      <div class="header-right">
       
       <div class="sort-container">
         <span>Sort by:</span>
         <select v-model="selectedSort" @change="sortProperties">
           <option>New Listing</option>
           <option>Price: Low to High</option>
           <option>Price: High to Low</option>
         </select>
       </div>
     </div>
      </div>
     </div>
     
    </div>

    <div class="property-cards">
      <div class="property-card" v-for="property in properties" :key="property.id">
        <div class="image-section">
          <img :src="property.image" alt="Property Image" />
          <div class="days-on-house">
            <span>{{ property.daysOnHouse }} days on house</span>
          </div>
          <div class="heart-icon">
            <font-awesome-icon :icon="['far', 'heart']" />
          </div>
        </div>
        <div class="info-section">
          <div class="propery-info">
            <div class="property-type">
            <span class="type-label"> <span class="live"></span> {{ property.type }}</span>
          </div>
          <div class="views">
            <span class="view-icon"><font-awesome-icon :icon="['far', 'eye']" /></span>
            <span>{{ property.views }}k</span>
          </div>
          </div>
          <div class="property-details">
            <div class="price">{{ property.price }}</div>
          <div class="details">
            <span><span class="span">{{ property.beds }}</span> Beds &nbsp; </span>
            <span><span class="span">{{ property.baths }}</span> Baths &nbsp;</span>
            <span><span class="span">{{ property.size }}</span> sqft.</span>
          </div>
          </div>
          <p class="title">{{ property.title }}</p>
          <p class="address">{{ property.address }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { library } from '@fortawesome/fontawesome-svg-core';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { faHeart, faEye } from '@fortawesome/free-regular-svg-icons';
import img from '../assets/image 9.png';
import img2 from '../assets/image 7.png';
import img3 from '../assets/image 8.png';
import img4 from '../assets/image 6.png';





library.add(faHeart, faEye);

const properties = ref([
  {
    id: 1,
    image: img,
    daysOnHouse: 5,
    type: "House of Sales",
    views: 2.3,
    price: "$3,349,000",
    beds: 4,
    baths: 3,
    size: 998,
    title: "2856 Meadow Park Ave, Henderson,",
    address: " NV 89052 (Real Tracs Mid) MLS-TN as distributed by MLS GRID"
  },
  {
    id: 2,
    image: img2,
    daysOnHouse: 10,
    type: "House of Sales",
    views: 1.5,
    price: "$2,899,000",
    beds: 3,
    baths: 2,
    size: 850,
    title: "1234 Oak St, Nashville,",
    address: "TN 37201 (Real Tracs Mid) MLS-TN as distributed by MLS GRID"
  },
  {
    id: 3,
    image: img3,
    daysOnHouse: 5,
    type: "House of Sales",
    views: 2.3,
    price: "$3,349,000",
    beds: 4,
    baths: 3,
    size: 998,
    title: "2856 Meadow Park Ave, Henderson,",
    address: " NV 89052 (Real Tracs Mid) MLS-TN as distributed by MLS GRID"
  },
  {
    id: 4,
    image: img4,
    daysOnHouse: 10,
    type: "House of Sales",
    views: 1.5,
    price: "$2,899,000",
    beds: 3,
    baths: 2,
    size: 850,
    title: "1234 Oak St, Nashville,",
    address: "TN 37201 (Real Tracs Mid) MLS-TN as distributed by MLS GRID"
  },
  {
    id: 5,
    image: img,
    daysOnHouse: 5,
    type: "House of Sales",
    views: 2.3,
    price: "$3,349,000",
    beds: 4,
    baths: 3,
    size: 998,
    title: "2856 Meadow Park Ave, Henderson,",
    address: " NV 89052 (Real Tracs Mid) MLS-TN as distributed by MLS GRID"
  },
  {
    id: 6,
    image: img3,
    daysOnHouse: 5,
    type: "House of Sales",
    views: 2.3,
    price: "$3,349,000",
    beds: 4,
    baths: 3,
    size: 998,
    title: "2856 Meadow Park Ave, Henderson,",
    address: " NV 89052 (Real Tracs Mid) MLS-TN as distributed by MLS GRID"
  },
]);

const selectedSort = ref('New Listing');

const sortProperties = () => {
  if (selectedSort.value === 'Price: Low to High') {
    properties.value.sort((a, b) => a.priceValue - b.priceValue);
  } else if (selectedSort.value === 'Price: High to Low') {
    properties.value.sort((a, b) => b.priceValue - a.priceValue);
  }
};
</script>

<style scoped>
.property-listings {
  padding: 20px;
  /* width: 50%; */
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px; /* Space below header */
}
.header-container {
  display: flex;
  justify-content: space-between;

}
.header-titles {
  text-align: left;
  line-height: 26px;
  display: flex;
  flex-direction: column;
  width: 100%;
}
.header-titles h3 {
  font-size: 18px;
}
.header-titles p {
  font-size: 14px;
}

.header-right {
  display: flex;
  align-items: center;
}

.home-count {
  color: grey;
  margin-right: 20px; /* Space between home count and sort */
}

.sort-container {
  display: flex;
  align-items: center;
  
}
.sort-container span{
  font-size: 14px;
  color: #00000066;
}

.sort-container select {
  margin-left: 0px;
  padding: 5px;
  border-radius: 5px;
  border: 0px solid #ccc;
  font-size: 14px;
  color: #0B5AA5;
  /* width: 105px; */
  font-weight: 500;
}

/* Property Cards */
.property-cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  cursor: pointer;
}

.property-card {
  background: white;
  border-radius: 10px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  width: 48%; /* Two cards in a row */
  margin-bottom: 30px; /* Space below cards */
  overflow: hidden;
  position: relative; /* For positioning icons */
}
.property-details {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 10px;
}

.image-section {
  position: relative;
}

.image-section img {
  width: 100%;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
}

.days-on-house {
  position: absolute;
  top: 15px;
  left: 15px;
  background: white;
  padding: 5px 10px;
  border-radius: 20px;
  font-size: 12px;
  font-weight: bold;
}

.heart-icon {
  position: absolute;
  top: 15px;
  right: 15px;
  cursor: pointer;
  color: rgb(248, 248, 248); /* Icon color */
}

.info-section {
  padding: 15px;
}
.propery-info {
  display: flex;
  justify-content: space-between;
}

.property-type {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.type-label {
  background: #fff;
  border-radius: 20px;
  padding: 5px 10px;
  border: 1px solid;
  font-size: 12px;
  display: flex;
  gap: 6px;
  align-items: center;
}
.type-label .live {
 height: 10px;
 width: 10px;
 background: #00B67B;
 display: block;
 border-radius: 50px;
}

.views {
  display: flex;
  align-items: center;
  margin: 5px 0; /* Space between rows */
  font-size: 12px;
  gap: 2px;
  align-items: center;
  font-size: 14px;
 
}
.view-icon {
  font-size: 14px;
}

.price {
  font-size: 18px;
  color: #0B5AA5;
  font-weight: bold;
  
}

.details {
  display: flex;
  justify-content: space-between;
  margin: 10px 0; /* Space between price and details */
  font-size: 12px;
  color: #00000080;
}
.details .span {
  font-size: 14px;
  color: #0B5AA5;
  font-weight: bold;
}

.address {
  margin-top: 5px; /* Space above address */
  font-size: 12px;
  text-align: left;
  color: #00000080;

}
.title {
  color: #00000080;
  font-weight: bold;
  text-align: left;
  font-size: 12px;
}

/* Responsive styles */
@media (max-width: 768px) {
  .property-card {
    width: 100%; /* Full width on mobile */
  }
  .header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: column;
  margin-bottom: 20px; /* Space below header */
}
}
</style>

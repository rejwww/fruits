<template>
  <CartComponent></CartComponent>
  <header class="header">
    <div class="header__items-container">
      <ul class="header__items">
        <li
          v-for="item in headerTitles"
          :key="item.id"
          class="header__item"
          :class="{
            'border-color-brown': !isLocationMain
          }"
        >
          <a
            class="header__item-link"
            :href="item.link"
            :class="{
              'link-color-brown': !isLocationMain
            }"
          >
            {{ item.name }}
          </a>
        </li>
      </ul>
    </div>

    <div class="header__actions-container">
      <button
        class="header__action header__cart"
        v-if="isLocationMain"
        @click="store.setCartValue(true)"
      >
        <img  style = "width:30px" src="../assets/icons/cart.svg" />             
      </button>

      <router-link to="/">
        <button class="header__action header__cart" v-if="!isLocationMain">
          <img style = "width:30px" src="../assets/icons/home-black.svg" />        
        </button>
      </router-link>

      <button
        class="header__action header__cart"
        v-if="!isLocationMain"
        @click="store.setCartValue(true)"
      >
        <img  style = "width:30px" src="../assets/icons/cart-black.svg" />     
      </button>
    </div>
  </header>
</template>
<script setup lang="ts">
import { computed, ref } from 'vue'
import { useRoute } from 'vue-router'
import { useMainStore } from '@/stores/index'
import CartComponent from './CartComponent.vue'
const store = useMainStore()

const isCartOpen = ref(store.isCartOpen)

const headerTitles = ref([
  {
    id: 1,
    name: 'О мастерской',
    link: '/#about'
  },
  {
    id: 2,
    name: 'Доставка',
    link: '/#delivery'
  },
  {
    id: 3,
    name: 'Коллекции',
    link: '/#collection'
  },
  {
    id: 4,
    name: 'Контакты',
    link: '/#footer'
  }
])

const route = useRoute()
const isLocationMain = computed(() => {
  if (route.path == '/') {
    return true
  } else return false
})

/** const isLocationMain = computed(() => {
    if(route.path == '/') {
        return true
    } else return false
}); */
</script>
<style lang="scss">
.border-color-brown {
  border: 1px solid #411212 !important;
  border-left: none !important;
}

.link-color-brown {
  color: #411212 !important;
}

.header {
  position: absolute;
  z-index: 33333;
  display: flex;
  width: 100%;
  justify-content: center;
  align-items: center;
  padding: 20px;                      

  .header__items-container {
    .header__items {
      display: flex;
      .header__item {
        border: 1px solid white;
        border-left: none;
        // border-right: none;
        .header__item-link {
          cursor: pointer;
          display: block;
          font-size: 30px;                              
          font-family: 'YanoneKaffeesatz-bold';
          color: white;
          padding: 8px 50px;                          
        }
      }
      .header__item:last-child {
        border-right: none !important;
      }
    }
  }

  .header__actions-container {
    position: absolute;
    display: flex;
    gap: 20px;
    right: 40px;
  }
}
</style>

  .header__actions-container {
    position: absolute;
    display: flex;
    gap: 20px;
    right: 40px;
  }
}
</style>

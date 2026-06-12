<template>
  <div>
    <header class="header">
      <div class="container header-inner">
        <div class="logo">🍳 Cooking Masterclass</div>
        <div style="font-weight:600; color:#4a5568;">
          Cart
          <span class="cart-badge">{{ totalItems }}</span>
        </div>
      </div>
    </header>

    <div class="container page-layout">
      <CourseCatalogue :courses="courses" @add-to-cart="addToCart" />
      <CartPanel
        :items="cartItems"
        :subtotal="subtotal"
        :tax="tax"
        :discount="discount"
        :grand-total="grandTotal"
        :coupon-code="couponCode"
        :coupon-message="couponMessage"
        @increase="increaseQty"
        @decrease="decreaseQty"
        @remove="removeItem"
        @clear-cart="clearCart"
        @apply-coupon="applyCoupon"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'
import CourseCatalogue from './components/CourseCatalogue.vue'
import CartPanel from './components/CartPanel.vue'
import { courses, TAX_RATE } from './data.js'

const cart = ref([])
const couponCode = ref('')
const couponMessage = ref('')

const CART_KEY = 'cooking_cart'

function loadCart() {
  const saved = localStorage.getItem(CART_KEY)
  if (saved) {
    try {
      cart.value = JSON.parse(saved)
    } catch {
      cart.value = []
    }
  }
}

function saveCart() {
  localStorage.setItem(CART_KEY, JSON.stringify(cart.value))
}

loadCart()
watch(cart, saveCart, { deep: true })

const cartItems = computed(() => {
  return cart.value.map(c => {
    const course = courses.find(x => x.id === c.id)
    return {
      ...course,
      quantity: c.quantity,
    }
  }).filter(item => item.id !== undefined)
})

const totalItems = computed(() => {
  return cart.value.reduce((sum, c) => sum + c.quantity, 0)
})

const subtotal = computed(() => {
  return cartItems.value.reduce((sum, item) => sum + item.price * item.quantity, 0)
})

const discountRate = computed(() => {
  if (couponCode.value === 'SAVE10') return 0.10
  if (couponCode.value === 'WELCOME15') return 0.15
  return 0
})

const discount = computed(() => {
  return subtotal.value * discountRate.value
})

const taxableAmount = computed(() => {
  return Math.max(0, subtotal.value - discount.value)
})

const tax = computed(() => {
  return taxableAmount.value * TAX_RATE
})

const grandTotal = computed(() => {
  return taxableAmount.value + tax.value
})

function addToCart(course) {
  if (course.soldOut) return
  const existing = cart.value.find(c => c.id === course.id)
  if (existing) {
    existing.quantity += 1
  } else {
    cart.value.push({ id: course.id, quantity: 1 })
  }
}

function increaseQty(id) {
  const item = cart.value.find(c => c.id === id)
  if (item) item.quantity += 1
}

function decreaseQty(id) {
  const item = cart.value.find(c => c.id === id)
  if (item) {
    item.quantity -= 1
    if (item.quantity <= 0) {
      cart.value = cart.value.filter(c => c.id !== id)
    }
  }
}

function removeItem(id) {
  cart.value = cart.value.filter(c => c.id !== id)
}

function clearCart() {
  cart.value = []
  couponCode.value = ''
  couponMessage.value = ''
}

function applyCoupon(code) {
  if (!code) {
    couponMessage.value = 'Please enter a coupon code.'
    return
  }
  const validCodes = ['SAVE10', 'WELCOME15']
  if (validCodes.includes(code.toUpperCase())) {
    couponCode.value = code.toUpperCase()
    couponMessage.value = ''
  } else {
    couponMessage.value = 'Invalid coupon code.'
  }
}
</script>

<template>
  <div class="cart-panel">
    <h2 class="section-title">Your Cart</h2>

    <div v-if="items.length === 0" class="cart-empty">
      <span class="cart-empty-icon">🛒</span>
      <p>Your cart is empty</p>
    </div>

    <div v-else>
      <div v-for="item in items" :key="item.id" class="cart-item">
        <div class="cart-item-thumb">{{ item.emoji }}</div>
        <div class="cart-item-info">
          <div class="cart-item-name">{{ item.name }}</div>
          <div class="cart-item-price">
            R {{ item.price.toLocaleString('en-ZA') }} each
          </div>
        </div>
        <div class="cart-item-controls">
          <button class="qty-btn" @click="$emit('decrease', item.id)" aria-label="Decrease quantity">−</button>
          <span class="qty-value">{{ item.quantity }}</span>
          <button class="qty-btn" @click="$emit('increase', item.id)" aria-label="Increase quantity">+</button>
          <button class="remove-btn" @click="$emit('remove', item.id)" aria-label="Remove item" title="Remove">🗑️</button>
        </div>
      </div>

      <div class="coupon-area">
        <input
          v-model="localCoupon"
          type="text"
          class="coupon-input"
          placeholder="Coupon code (e.g. SAVE10)"
          @keyup.enter="$emit('apply-coupon', localCoupon.trim())"
        />
        <button class="btn btn-secondary btn-small" @click="$emit('apply-coupon', localCoupon.trim())">
          Apply
        </button>
      </div>
      <div v-if="couponMessage" style="font-size:0.8rem; margin-bottom:8px; color:#e53e3e;">
        {{ couponMessage }}
      </div>

      <div class="summary-block">
        <div class="summary-row">
          <span>Subtotal</span>
          <span>R {{ subtotal.toLocaleString('en-ZA', { minimumFractionDigits: 2 }) }}</span>
        </div>
        <div v-if="discount > 0" class="summary-row discount-row">
          <span>Discount ({{ couponCode }})</span>
          <span>− R {{ discount.toLocaleString('en-ZA', { minimumFractionDigits: 2 }) }}</span>
        </div>
        <div class="summary-row">
          <span>Tax (15%)</span>
          <span>R {{ tax.toLocaleString('en-ZA', { minimumFractionDigits: 2 }) }}</span>
        </div>
        <div class="summary-row total">
          <span>Grand Total</span>
          <span>R {{ grandTotal.toLocaleString('en-ZA', { minimumFractionDigits: 2 }) }}</span>
        </div>
      </div>

      <button class="btn btn-danger btn-small clear-cart-btn" @click="$emit('clear-cart')">
        Clear Cart
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
  items: {
    type: Array,
    required: true,
  },
  subtotal: {
    type: Number,
    required: true,
  },
  tax: {
    type: Number,
    required: true,
  },
  discount: {
    type: Number,
    required: true,
  },
  grandTotal: {
    type: Number,
    required: true,
  },
  couponCode: {
    type: String,
    default: '',
  },
  couponMessage: {
    type: String,
    default: '',
  },
})

const localCoupon = ref(props.couponCode)

watch(() => props.couponCode, (val) => {
  localCoupon.value = val
})

defineEmits(['increase', 'decrease', 'remove', 'clear-cart', 'apply-coupon'])
</script>

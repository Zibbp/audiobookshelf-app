<template>
  <button class="icon-btn rounded-md flex items-center justify-center h-9 w-9 relative" :disabled="disabled || loading" :class="className" :type="type" @mousedown.prevent @click="clickBtn">
    <div v-if="loading" class="text-fg absolute top-0 left-0 w-full h-full flex items-center justify-center text-opacity-100">
      <svg class="animate-spin" style="width: 24px; height: 24px" viewBox="0 0 24 24">
        <path fill="currentColor" d="M12,4V2A10,10 0 0,0 2,12H4A8,8 0 0,1 12,4Z" />
      </svg>
    </div>
    <span v-else class="material-symbols text-2xl" :class="{ fill: !outlined }" :style="{ fontSize }">{{ icon }}</span>
  </button>
</template>

<script>
export default {
  props: {
    icon: String,
    type: {
      type: String,
      default: 'button'
    },
    disabled: Boolean,
    bgColor: {
      type: String,
      default: 'primary'
    },
    outlined: Boolean,
    borderless: Boolean,
    loading: Boolean
  },
  data() {
    return {}
  },
  computed: {
    className() {
      var classes = []
      if (!this.borderless) {
        classes.push(`bg-${this.bgColor} border border-gray-600`)
      }
      return classes.join(' ')
    },
    fontSize() {
      if (this.icon === 'edit') return '1.25rem'
      return '1.4rem'
    }
  },
  methods: {
    clickBtn(e) {
      if (this.disabled || this.loading) {
        e.preventDefault()
        return
      }
      e.preventDefault()
      this.$emit('click')
      e.stopPropagation()
    }
  },
  mounted() {}
}
</script>

<style>
button.icon-btn:disabled {
  cursor: not-allowed;
}
button.icon-btn::before {
  content: '';
  position: absolute;
  border-radius: 6px;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(255, 255, 255, 0);
  transition: all 0.1s ease-in-out;
}
button.icon-btn:hover:not(:disabled)::before {
  background-color: rgba(255, 255, 255, 0.1);
}
button.icon-btn:disabled::before {
  background-color: rgba(0, 0, 0, 0.2);
}
button.icon-btn:disabled span {
  color: #777;
}
</style>

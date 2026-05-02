<template>
  <div class="relative inline-block" @mouseenter="show" @mouseleave="hide">
    <slot />

    <Transition :name="`tt-${placement}`">
      <span
        v-if="visible"
        class="absolute z-50 whitespace-nowrap rounded-md bg-primary px-4 py-1.5 text-xs font-semibold text-slate-200 pointer-events-none"
        :class="placementClasses"
      >
        {{ text }}
        <span class="absolute h-[7px] w-[7px] rotate-45 bg-primary" :class="arrowClasses" />
      </span>
    </Transition>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue'

const props = defineProps({
  text: { type: String, required: true },
  placement: {
    type: String,
    default: 'top',
    validator: (v) => ['top', 'bottom', 'left', 'right'].includes(v),
  },
})

const visible = ref(false)
const show = () => (visible.value = true)
const hide = () => (visible.value = false)

const placementClasses = computed(
  () =>
    ({
      top: 'bottom-[calc(100%+10px)] left-1/2 -translate-x-1/2',
      bottom: 'top-[calc(100%+10px)] left-1/2 -translate-x-1/2',
      left: 'top-1/2 right-[calc(100%+10px)] -translate-y-1/2',
      right: 'top-1/2 left-[calc(100%+10px)] -translate-y-1/2',
    })[props.placement],
)

const arrowClasses = computed(
  () =>
    ({
      top: 'left-1/2 -bottom-[3px] -translate-x-1/2',
      bottom: 'left-1/2 -top-[3px] -translate-x-1/2',
      left: 'top-1/2 -right-[3px] -translate-y-1/2',
      right: 'top-1/2 -left-[3px] -translate-y-1/2',
    })[props.placement],
)
</script>

<style scoped>
.tt-top-enter-active,
.tt-top-leave-active,
.tt-bottom-enter-active,
.tt-bottom-leave-active,
.tt-left-enter-active,
.tt-left-leave-active,
.tt-right-enter-active,
.tt-right-leave-active {
  transition:
    opacity 0.18s ease,
    transform 0.18s ease;
}

.tt-top-enter-from,
.tt-top-leave-to {
  opacity: 0;
  transform: translateX(-50%) translateY(8px);
}

.tt-bottom-enter-from,
.tt-bottom-leave-to {
  opacity: 0;
  transform: translateX(-50%) translateY(-8px);
}

.tt-left-enter-from,
.tt-left-leave-to {
  opacity: 0;
  transform: translateY(-50%) translateX(8px);
}

.tt-right-enter-from,
.tt-right-leave-to {
  opacity: 0;
  transform: translateY(-50%) translateX(-8px);
}
</style>

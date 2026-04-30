<template>
  <ul class="space-y-1">
    <li
      v-for="category in categories"
      :key="category.name"
      class="flex items-center gap-3 rounded-lg px-3 py-2.5 text-sm font-semibold text-gray-800 transition-all hover:bg-rose-50 hover:text-rose-500 cursor-pointer group"
      @click="emit('select', category.name)"
    >
      <component
        :is="category.icon"
        class="h-4 w-4 text-gray-400 group-hover:text-rose-400 transition-colors shrink-0"
      />
      <span>{{ category.name }}</span>
    </li>
  </ul>
</template>

<script setup>
import {
  Camera,
  Gamepad2,
  Headphones,
  Monitor,
  MonitorDot,
  Network,
  Package,
  Printer,
  Smartphone,
  Speaker,
  Wrench,
} from '@lucide/vue'

const emit = defineEmits(['select'])

const categories = [
  { name: 'Laptop', icon: Monitor },
  { name: 'Headphones', icon: Headphones },
  { name: 'Desktop', icon: MonitorDot },
  { name: 'Mobile & Tablets', icon: Smartphone },
  { name: 'Network', icon: Network },
  { name: 'Accessories', icon: Package },
  { name: 'Software', icon: Wrench },
  { name: 'Camera & Security', icon: Camera },
  { name: 'Speaker & Audio', icon: Speaker },
  { name: 'Printer', icon: Printer },
  { name: 'Game & Console', icon: Gamepad2 },
]
</script>

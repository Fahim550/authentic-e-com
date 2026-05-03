<template>
  <section class="px-4 py-6 sm:px-6 lg:px-14 bg-white">
    <div class="relative overflow-hidden rounded-2xl bg-primary p-10">
      <!-- <div class="absolute inset-0 pointer-events-none">
        <div
          class="absolute right-0 top-0 h-full w-1/2 bg-gradient-to-l from-accent/30 via-accent/20 to-transparent"
        />
      </div> -->

      <div
        className="absolute -top-32 -right-32 w-120 h-120 bg-accent/20 blur-3xl rounded-full"
      ></div>
      <div
        className="absolute -bottom-32 -left-32 w-120 h-120 bg-blue-500/10 blur-3xl rounded-full"
      ></div>

      <div class="absolute right-16 top-6 pointer-events-none select-none">
        <div class="absolute right-28 top-12 w-3 h-3 bg-white/20 rotate-45 rounded-sm" />
        <div
          class="absolute right-10 top-8 w-0 h-0"
          style="
            border-left: 7px solid transparent;
            border-right: 7px solid transparent;
            border-bottom: 12px solid rgba(255, 255, 255, 0.15);
          "
        />
        <!-- large circle solid -->
        <div class="absolute right-20 top-38 w-16 h-16 rounded-full bg-white/10" />
        <div
          class="absolute right-0 top-20 w-16 h-16 rounded-full border-2 border-dashed border-white/15"
        />
        <div class="absolute right-36 top-24 w-10 h-10 rounded-full bg-white/10" />
        <div
          class="absolute right-6 top-30 w-10 h-10 border-b-2 border-l-2 border-white/20 rounded-bl-full"
        />
      </div>

      <div class="relative z-10 max-w-xl">
        <div
          class="inline-flex items-center gap-2 border border-white/20 bg-white/10 transition-colors rounded-full px-3 py-1 mb-4"
        >
          <House class="w-6 h-6 text-white" />

          <span class="text-xs text-white font-medium">Partner with Entry</span>
        </div>

        <!-- Heading -->
        <h2 class="text-3xl font-bold text-white mb-3 leading-snug">Become a Seller on Entry</h2>

        <!-- Description -->
        <p class="text-lg text-white/80 mb-7 max-w-2xl">
          Join our marketplace and reach thousands of customers. Sell your baby products with ease
          and grow your business today.
        </p>

        <!-- Buttons -->
        <div class="flex flex-col lg:flex-row w-full items-center gap-3">
          <button
            class="inline-flex items-center w-full text-center justify-center gap-2 bg-accent hover:bg-accent/90 text-white text-sm font-semibold px-7 py-2.5 rounded-full transition-colors duration-200 cursor-pointer"
          >
            Apply Now
            <ArrowUpRight class="w-6 h-6" />
          </button>

          <button
            class="inline-flex items-center w-full text-center justify-center gap-2 bg-white/10 hover:bg-white/20 text-white text-sm font-medium px-7 py-2.5 rounded-full border border-white/15 transition-colors duration-200 cursor-pointer"
          >
            Learn More
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ArrowUpRight, House } from '@lucide/vue'

// No logic needed — purely presentational
</script>

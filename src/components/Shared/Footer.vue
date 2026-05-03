<template>
  <footer class="bg-primary text-white">
    <!-- Top CTA strip -->
    <div class="border-b border-white/10">
      <div
        class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-14 py-8 flex flex-col sm:flex-row items-center justify-between gap-4"
      >
        <div class="flex items-center gap-3">
          <div
            class="w-10 h-10 rounded-full bg-primary/50 border-2 border-border flex items-center justify-center"
          >
            <Mail class="w-6 h-6" />
          </div>
          <div>
            <p class="text-sm font-semibold text-white">Subscribe to our newsletter</p>
            <p class="text-xs text-white/40">Get deals, new arrivals & updates.</p>
          </div>
        </div>
        <form class="flex w-full sm:w-auto gap-2" @submit.prevent>
          <input
            type="email"
            placeholder="Enter your email"
            class="flex-1 sm:w-64 bg-white/5 border border-white/10 rounded-full px-4 py-2 text-sm text-white placeholder-white/30 outline-none focus:border-primary transition-colors"
          />
          <button
            type="submit"
            class="bg-primary hover:bg-primary/90 text-white text-sm font-semibold px-5 py-2 rounded-full transition-colors whitespace-nowrap"
          >
            Subscribe
          </button>
        </form>
      </div>
    </div>

    <!-- Main footer grid -->
    <div
      class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-14 py-14 grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-5 gap-10"
    >
      <!-- Brand col -->
      <div class="col-span-2 sm:col-span-3 lg:col-span-2">
        <a href="/" class="inline-flex items-center gap-2 mb-4">
          <div class="w-8 h-8 bg-primary rounded-lg flex items-center justify-center"></div>
          <span class="text-xl font-bold tracking-tight text-white">Authentic</span>
        </a>
        <p class="text-sm text-white/45 leading-relaxed max-w-xs mb-6">
          Your one-stop marketplace for electronics, fashion, beauty & more. Trusted by thousands of
          happy customers.
        </p>

        <!-- Contact info -->
        <ul class="space-y-2.5">
          <li class="flex items-center gap-2.5 text-sm text-white/50">
            <Phone class="w-5 h-5" />
            09696779933
          </li>
          <li class="flex items-center gap-2.5 text-sm text-white/50">
            <Mail class="w-5 h-5" />
            support@authentic.com
          </li>
          <li class="flex items-start gap-2.5 text-sm text-white/50">
            <MapPin class="w-5 h-5" />
            House#3/A, Lichu Bagan Road,Joar Shara Bazar,Dhaka-1230
          </li>
        </ul>
      </div>

      <!-- Quick Links -->
      <div>
        <h3 class="text-xs font-semibold uppercase tracking-widest text-white/30 mb-5">
          Quick Links
        </h3>
        <ul class="space-y-3">
          <li v-for="link in quickLinks" :key="link">
            <a href="#" class="text-sm text-white/55 hover:text-white transition-colors">{{
              link
            }}</a>
          </li>
        </ul>
      </div>

      <!-- Customer Service -->
      <div>
        <h3 class="text-xs font-semibold uppercase tracking-widest text-white/30 mb-5">
          Customer Service
        </h3>
        <ul class="space-y-3">
          <li v-for="link in customerLinks" :key="link">
            <a href="#" class="text-sm text-white/55 hover:text-white transition-colors">{{
              link
            }}</a>
          </li>
        </ul>
      </div>

      <!-- Company -->
      <div>
        <h3 class="text-xs font-semibold uppercase tracking-widest text-white/30 mb-5">Company</h3>
        <ul class="space-y-3">
          <li v-for="link in companyLinks" :key="link">
            <a href="#" class="text-sm text-white/55 hover:text-white transition-colors">{{
              link
            }}</a>
          </li>
        </ul>

        <!-- App download -->
        <!-- <h3 class="text-xs font-semibold uppercase tracking-widest text-white/30 mt-8 mb-4">
          Get the App
        </h3>
        <div class="flex flex-col gap-2">
          <a
            href="#"
            class="flex items-center gap-2 bg-white/5 hover:bg-white/10 border border-white/10 rounded-lg px-3 py-2 transition-colors"
          >
            <svg class="w-5 h-5 text-white/60" viewBox="0 0 24 24" fill="currentColor">
              <path
                d="M18.71 19.5c-.83 1.24-1.71 2.45-3.05 2.47-1.34.03-1.77-.79-3.29-.79-1.53 0-2 .77-3.27.82-1.31.05-2.3-1.32-3.14-2.53C4.25 17 2.94 12.45 4.7 9.39c.87-1.52 2.43-2.48 4.12-2.51 1.28-.02 2.5.87 3.29.87.78 0 2.26-1.07 3.8-.91.65.03 2.47.26 3.64 1.98-.09.06-2.17 1.28-2.15 3.81.03 3.02 2.65 4.03 2.68 4.04-.03.07-.42 1.44-1.38 2.83M13 3.5c.73-.83 1.94-1.46 2.94-1.5.13 1.17-.34 2.35-1.04 3.19-.69.85-1.83 1.51-2.95 1.42-.15-1.15.41-2.35 1.05-3.11z"
              />
            </svg>
            <div class="leading-tight">
              <p class="text-[9px] text-white/35">Download on the</p>
              <p class="text-xs font-semibold text-white/80">App Store</p>
            </div>
          </a>
          <a
            href="#"
            class="flex items-center gap-2 bg-white/5 hover:bg-white/10 border border-white/10 rounded-lg px-3 py-2 transition-colors"
          >
            <svg class="w-5 h-5 text-white/60" viewBox="0 0 24 24" fill="currentColor">
              <path
                d="M3.18 23.76c.3.17.65.19.98.08l12.76-7.37-2.79-2.79-10.95 10.08zM.46 1.12C.17 1.45 0 1.94 0 2.58v18.84c0 .64.17 1.13.46 1.46l.08.07 10.56-10.56v-.25L.54 1.05l-.08.07zM20.51 10.17l-2.82-1.63-3.12 3.12 3.12 3.12 2.84-1.64c.81-.47.81-1.23-.02-1.97zM3.18.24L15.94 7.6l-2.79 2.79L3.18.32c-.33-.19-.68-.17-.98.08l.98-.16z"
              />
            </svg>
            <div class="leading-tight">
              <p class="text-[9px] text-white/35">Get it on</p>
              <p class="text-xs font-semibold text-white/80">Google Play</p>
            </div>
          </a>
        </div> -->
      </div>
    </div>

    <!-- Payment methods + social -->
    <div class="border-t border-white/10">
      <div
        class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-14 py-6 flex flex-col sm:flex-row items-center justify-between gap-4"
      >
        <!-- Payment icons -->
        <!-- <div class="flex items-center gap-2 flex-wrap justify-center sm:justify-start">
          <span class="text-xs text-white/30 mr-1">We Accept:</span>
          <div
            v-for="pay in paymentMethods"
            :key="pay.name"
            class="bg-white/10 border border-white/10 rounded-md px-2.5 py-1 text-xs font-bold"
            :style="{ color: pay.color }"
          >
            {{ pay.name }}
          </div>
        </div> -->
        <p class="text-white/25 flex items-center gap-1 text-sm">
          <Copyright class="w-6 h-6" /> {{ new Date().getFullYear() }} Authentic. All rights
          reserved.
        </p>

        <!-- Social icons -->
        <div class="flex items-center gap-3">
          <a
            v-for="social in socials"
            :key="social.name"
            href="#"
            class="w-8 h-8 rounded-full bg-white/5 hover:bg-primary/20 border border-white/10 hover:border-primary/40 flex items-center justify-center transition-colors"
            :aria-label="social.name"
          >
            <svg
              class="w-3.5 h-3.5 text-white/50 hover:text-primary"
              viewBox="0 0 24 24"
              fill="currentColor"
              v-html="social.icon"
            />
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup>
import { Copyright, Mail, MapPin, Phone } from '@lucide/vue'

const quickLinks = ['Home', 'Shop', 'New Arrivals', 'Best Sellers', 'Sale & Offers', 'Gift Cards']

const customerLinks = [
  'My Account',
  'Track My Order',
  'Returns & Refunds',
  'Shipping Info',
  'FAQ',
  'Contact Us',
]

const companyLinks = [
  'About Us',
  'Careers',
  'Blog',
  'Become a Seller',
  'Privacy Policy',
  'Terms of Service',
]

const paymentMethods = [
  { name: 'VISA', color: '#1a73e8' },
  { name: 'MC', color: '#eb001b' },
  { name: 'PayPal', color: '#003087' },
  { name: 'Apple Pay', color: '#f5f5f5' },
  { name: 'Google Pay', color: '#4285f4' },
  { name: 'Stripe', color: '#635bff' },
]

const socials = [
  {
    name: 'Facebook',
    icon: '<path d="M18 2h-3a5 5 0 00-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 011-1h3z"/>',
  },
  {
    name: 'Instagram',
    icon: '<rect x="2" y="2" width="20" height="20" rx="5" ry="5"/><path d="M16 11.37A4 4 0 1112.63 8 4 4 0 0116 11.37z" fill="none" stroke="currentColor" stroke-width="2"/><line x1="17.5" y1="6.5" x2="17.51" y2="6.5" stroke="currentColor" stroke-width="2"/>',
  },

  {
    name: 'YouTube',
    icon: '<path d="M22.54 6.42a2.78 2.78 0 00-1.95-1.96C18.88 4 12 4 12 4s-6.88 0-8.59.46a2.78 2.78 0 00-1.95 1.96A29 29 0 001 12a29 29 0 00.46 5.58A2.78 2.78 0 003.41 19.6C5.12 20 12 20 12 20s6.88 0 8.59-.46a2.78 2.78 0 001.95-1.95A29 29 0 0023 12a29 29 0 00-.46-5.58z"/><polygon points="9.75 15.02 15.5 12 9.75 8.98 9.75 15.02"/>',
  },
]
</script>

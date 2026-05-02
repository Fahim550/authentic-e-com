<template>
  <section class="">
    <HeroSection />
    <Categories />
    <FeatureProduct />
    <TrandingProduct />
    <SpecialOfferBanner />
    <NewArrivalsProduct />
    <BestDeals />
    <BeComeSeller />
  </section>
</template>

<script setup>
import BeComeSeller from '@/components/home/BeComeSeller.vue'
import BestDeals from '@/components/home/BestDeals.vue'
import NewArrivalsProduct from '@/components/home/NewArrivalsProduct.vue'
import TrandingProduct from '@/components/home/TrandingProduct.vue'
import Categories from '../components/home/Categories.vue'
import FeatureProduct from '../components/home/FeatureProduct.vue'
import HeroSection from '../components/home/HeroSection.vue'
import SpecialOfferBanner from '../components/home/SpecialOfferBanner.vue'
</script>

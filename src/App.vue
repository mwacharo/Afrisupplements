
<script setup>
import { ref, computed } from 'vue'
import {
  Truck,
  Wallet,
  ShieldCheck,
  PackageCheck,
  ArrowRight,
  CheckCircle2,
  PhoneCall,
  ShoppingBag,
  ChevronDown,
  Leaf,
  MapPin,
  Menu
} from 'lucide-vue-next'

const product = {
  name: 'Strong Man Herbal Syrup',
  price: 3500,
  currency: 'KSh',
  image: '/images/strongmanredirect.png',
  url: 'https://afrisupplements.storeep.com/products/strong-man'
}

const formattedPrice = computed(() => {
  return `${product.currency} ${product.price.toLocaleString()}`
})

const orderUrl = computed(() => {
  const destination = new URL(product.url)
  const params = new URLSearchParams(window.location.search)

  const allowed = [
    'utm_source',
    'utm_medium',
    'utm_campaign',
    'utm_content',
    'utm_term'
  ]

  allowed.forEach(key => {
    if (params.has(key)) {
      destination.searchParams.set(key, params.get(key))
    }
  })

  return destination.toString()
})

const benefits = [
  {
    icon: Wallet,
    title: 'Pay on Delivery',
    description: 'No upfront payment required.'
  },
  {
    icon: Truck,
    title: 'Nationwide Delivery',
    description: 'Delivery across Kenya.'
  },
  {
    icon: PackageCheck,
    title: 'Discreet Packaging',
    description: 'Your privacy matters to us.'
  },
  {
    icon: ShieldCheck,
    title: 'Convenient Shopping',
    description: 'Simple online ordering.'
  }
]

const steps = [
  {
    icon: ShoppingBag,
    title: 'Place Your Order',
    description: 'Provide your name, phone number and delivery location.'
  },
  {
    icon: PhoneCall,
    title: 'Confirm Your Order',
    description: 'Our team will contact you to confirm your order and availability.'
  },
  {
    icon: Truck,
    title: 'Receive Your Package',
    description: 'Your package is delivered to your agreed location.'
  },
  {
    icon: Wallet,
    title: 'Pay on Delivery',
    description: 'Make payment when you receive your order.'
  }
]

const faqs = [
  {
    question: 'Do I need to pay upfront?',
    answer: 'No. You can place your order online and make payment upon delivery.'
  },
  {
    question: 'Do you deliver outside Nairobi?',
    answer: 'Yes. Delivery is available across Kenya. Delivery times and any applicable charges will be confirmed before dispatch.'
  },
  {
    question: 'Is the packaging discreet?',
    answer: 'Yes. Orders are packaged with your privacy in mind.'
  },
  {
    question: 'How do I place an order?',
    answer: 'Click any Order Now button to visit our official online store and complete your order.'
  },
  {
    question: 'Where can I find product information?',
    answer: 'Visit our online store for product ingredients, usage instructions, precautions and other product information.'
  }
]

const activeFaq = ref(null)

function toggleFaq(index) {
  activeFaq.value = activeFaq.value === index
    ? null
    : index
}

function orderNow() {
  window.location.assign(orderUrl.value)
}
</script>

<template>
  <div class="min-h-screen bg-white text-slate-900 pb-24 md:pb-0">

    <!-- Announcement bar -->
    <div class="bg-green-950 px-4 py-3 text-center
                text-xs font-medium text-white sm:text-sm">
      🇰🇪 Nationwide Delivery &nbsp;•&nbsp;
      No Upfront Payment
    </div>

    <!-- Navigation -->
    <header class="border-b border-green-100 bg-white">
      <div class="mx-auto flex max-w-7xl items-center
                  justify-between px-5 py-5">

        <div>
          <div class="flex items-center gap-2">
            <Leaf class="h-7 w-7 text-green-700" />

            <span class="text-xl font-black tracking-tight
                         text-green-950 sm:text-2xl">
              Afri<span class="text-green-600">Supplements</span>
            </span>
          </div>

          <p class="mt-1 text-[9px] tracking-[0.2em]
                    text-slate-500">
            NATURAL HEALTH & WELLNESS
          </p>
        </div>

        <button
          @click="orderNow"
          class="hidden rounded-xl bg-green-700 px-6
                 py-3 font-semibold text-white
                 hover:bg-green-800 md:block"
        >
          Shop Now
        </button>
      </div>
    </header>

    <!-- Hero -->
    <section class="bg-gradient-to-br from-green-50
                    via-white to-lime-50">

      <div class="mx-auto grid max-w-7xl items-center
                  gap-10 px-5 py-12 md:grid-cols-2
                  md:py-24">

        <!-- Content -->
        <div class="order-2 md:order-1">

          <div class="mb-5 inline-flex items-center gap-2
                      rounded-full border border-green-200
                      bg-green-100 px-4 py-2 text-xs
                      font-bold text-green-800">
            <ShieldCheck class="h-4 w-4" />
            NO UPFRONT PAYMENT
          </div>

          <h1 class="text-4xl font-black leading-tight
                     tracking-tight text-green-950
                     sm:text-5xl lg:text-6xl">
            Order With
            Confidence.

            <span class="mt-2 block text-green-600">
              Receive First.
              Pay Later.
            </span>
          </h1>

          <h2 class="mt-6 text-2xl font-bold text-slate-800">
            {{ product.name }}
          </h2>

          <p class="mt-4 text-base leading-relaxed
                    text-slate-600 sm:text-lg">
            Discover our herbal formulation and enjoy
            convenient online shopping, discreet packaging
            and payment upon delivery.
          </p>

          <!-- Product price -->
          <div class="mt-6">
            <p class="text-sm text-slate-500">
              Product price
            </p>

            <span class="text-4xl font-black text-green-900">
              {{ formattedPrice }}
            </span>
          </div>

          <!-- COD promotion -->
          <div class="mt-6 rounded-2xl border
                      border-green-200 bg-green-100 p-5">

            <div class="flex items-center gap-4">
              <Wallet class="h-10 w-10 text-green-700" />

              <div>
                <p class="text-sm font-medium text-green-800">
                  Upfront payment
                </p>

                <p class="text-3xl font-black text-green-950">
                  KSh 0
                </p>

                <p class="text-sm text-green-800">
                  Pay when your order arrives.
                </p>
              </div>
            </div>
          </div>

          <!-- CTA -->
          <button
            @click="orderNow"
            class="mt-6 flex w-full items-center
                   justify-center gap-3 rounded-xl
                   bg-green-700 px-6 py-5 text-lg
                   font-bold text-white shadow-lg
                   shadow-green-900/10 transition
                   hover:bg-green-800 active:scale-[0.98]"
          >
            ORDER NOW — PAY ON DELIVERY
            <ArrowRight class="h-5 w-5 shrink-0" />
          </button>

          <p class="mt-3 text-center text-xs text-slate-500">
            Continue to the AfriSupplements online store.
          </p>
        </div>

        <!-- Product photography -->
        <div class="order-1 md:order-2">

          <div class="relative overflow-hidden rounded-3xl
                      border border-green-100 bg-white
                      p-6 shadow-xl shadow-green-900/5">

            <img
              :src="product.image"
              :alt="product.name"
              class="mx-auto aspect-square w-full
                     max-w-lg object-contain"
              fetchpriority="high"
            />

            <div class="absolute right-4 top-4 rounded-full
                        bg-green-700 px-4 py-2 text-xs
                        font-bold text-white">
              AVAILABLE IN KENYA
            </div>
          </div>

          <div class="mt-4 flex items-center justify-center
                      gap-2 text-sm text-slate-600">
            <MapPin class="h-4 w-4 text-green-700" />
            Delivery across Kenya
          </div>
        </div>
      </div>
    </section>

    <!-- Trust signals -->
    <section class="border-y border-slate-100 bg-white">
      <div class="mx-auto grid max-w-7xl grid-cols-2
                  gap-6 px-5 py-10 md:grid-cols-4">

        <div
          v-for="benefit in benefits"
          :key="benefit.title"
          class="text-center"
        >
          <div class="mx-auto mb-4 flex h-14 w-14
                      items-center justify-center
                      rounded-2xl bg-green-100">

            <component
              :is="benefit.icon"
              class="h-7 w-7 text-green-700"
            />
          </div>

          <h3 class="font-bold text-green-950">
            {{ benefit.title }}
          </h3>

          <p class="mt-2 text-sm text-slate-500">
            {{ benefit.description }}
          </p>
        </div>
      </div>
    </section>

    <!-- Ordering process -->
    <section class="bg-slate-50 px-5 py-16 md:py-24">

      <div class="mx-auto max-w-6xl">

        <div class="mb-12 text-center">
          <p class="text-sm font-bold tracking-widest
                    text-green-700">
            SIMPLE & CONVENIENT
          </p>

          <h2 class="mt-3 text-3xl font-black
                     text-green-950 md:text-4xl">
            How It Works
          </h2>

          <p class="mt-3 text-slate-500">
            Four simple steps to receive your order.
          </p>
        </div>

        <div class="grid gap-5 sm:grid-cols-2
                    lg:grid-cols-4">

          <div
            v-for="(step, index) in steps"
            :key="step.title"
            class="relative rounded-2xl border
                   border-slate-200 bg-white p-6"
          >
            <div class="absolute right-5 top-5 text-4xl
                        font-black text-green-100">
              0{{ index + 1 }}
            </div>

            <component
              :is="step.icon"
              class="mb-5 h-8 w-8 text-green-700"
            />

            <h3 class="font-bold text-green-950">
              {{ step.title }}
            </h3>

            <p class="mt-3 text-sm leading-relaxed
                      text-slate-600">
              {{ step.description }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Why choose us -->
    <section class="bg-green-950 px-5 py-16 text-white">
      <div class="mx-auto grid max-w-6xl items-center
                  gap-10 md:grid-cols-2">

        <div>
          <p class="text-sm font-bold tracking-widest
                    text-green-300">
            SHOP WITH CONFIDENCE
          </p>

          <h2 class="mt-4 text-3xl font-black md:text-4xl">
            Your Convenience.
            <br />
            Our Priority.
          </h2>

          <p class="mt-4 leading-relaxed text-green-100">
            We make online shopping simple, private
            and convenient for customers across Kenya.
          </p>
        </div>

        <div class="space-y-4">

          <div
            v-for="item in [
              'No upfront payment required',
              'Convenient online ordering',
              'Discreet product packaging',
              'Customer order confirmation',
              'Delivery across Kenya'
            ]"
            :key="item"
            class="flex items-center gap-3 rounded-xl
                   border border-white/10 bg-white/5 p-4"
          >
            <CheckCircle2
              class="h-5 w-5 shrink-0 text-green-400"
            />

            <span>{{ item }}</span>
          </div>
        </div>
      </div>
    </section>

    <!-- Frequently asked questions -->
    <section class="px-5 py-16 md:py-24">
      <div class="mx-auto max-w-3xl">

        <h2 class="mb-8 text-center text-3xl font-black
                   text-green-950">
          Frequently Asked Questions
        </h2>

        <div class="space-y-3">

          <div
            v-for="(faq, index) in faqs"
            :key="index"
            class="overflow-hidden rounded-xl
                   border border-slate-200"
          >
            <button
              @click="toggleFaq(index)"
              :aria-expanded="activeFaq === index"
              class="flex w-full items-center justify-between
                     gap-4 p-5 text-left font-semibold
                     text-slate-800 hover:bg-slate-50"
            >
              {{ faq.question }}

              <ChevronDown
                :class="[
                  'h-5 w-5 shrink-0 transition-transform',
                  activeFaq === index ? 'rotate-180' : ''
                ]"
              />
            </button>

            <div
              v-if="activeFaq === index"
              class="px-5 pb-5 text-sm leading-relaxed
                     text-slate-600"
            >
              {{ faq.answer }}
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Final call to action -->
    <section class="bg-green-50 px-5 py-16">
      <div class="mx-auto max-w-2xl text-center">

        <h2 class="text-3xl font-black text-green-950
                   md:text-4xl">
          Ready to Place Your Order?
        </h2>

        <p class="mt-4 leading-relaxed text-slate-600">
          Order conveniently online and pay when your
          package arrives. Please ensure you are available
          to receive and pay for your order.
        </p>

        <div class="my-6 text-4xl font-black text-green-900">
          {{ formattedPrice }}
        </div>

        <button
          @click="orderNow"
          class="flex w-full items-center justify-center
                 gap-3 rounded-xl bg-green-700 px-6 py-5
                 text-lg font-bold text-white
                 hover:bg-green-800"
        >
          PROCEED TO ORDER
          <ArrowRight class="h-5 w-5" />
        </button>

        <p class="mt-4 text-sm text-slate-500">
          No online payment required.
        </p>
      </div>
    </section>

    <!-- Footer -->
    <footer class="bg-green-950 px-5 py-10
                   text-center text-green-100">

      <h3 class="text-xl font-bold text-white">
        AfriSupplements
      </h3>

      <p class="mt-2 text-xs tracking-widest">
        NATURAL HEALTH & WELLNESS
      </p>

      <a
        :href="product.url"
        class="mt-5 inline-block text-sm underline"
      >
        Visit our online store
      </a>

      <p class="mt-6 text-xs text-green-200">
        Review product ingredients, usage instructions
        and precautions before use.
      </p>

      <p class="mt-6 text-xs">
        © {{ new Date().getFullYear() }} AfriSupplements.
        All rights reserved.
      </p>
    </footer>

    <!-- Sticky mobile purchase bar -->
    <div class="fixed inset-x-0 bottom-0 z-50
                border-t border-slate-200 bg-white
                px-4 py-3 shadow-2xl md:hidden">

      <div class="flex items-center gap-4">

        <div class="shrink-0">
          <p class="text-xl font-black text-green-950">
            {{ formattedPrice }}
          </p>

          <p class="text-[11px] text-green-700">
            Pay on delivery
          </p>
        </div>

        <button
          @click="orderNow"
          class="flex flex-1 items-center justify-center
                 gap-2 rounded-xl bg-green-700
                 px-4 py-4 text-sm font-bold text-white"
        >
          ORDER NOW
          <ArrowRight class="h-4 w-4" />
        </button>
      </div>
    </div>

  </div>
</template>

<template>
  <PatternSection>
    <main class="flex-grow">
      <div class="container mx-auto py-12 px-4 sm:px-6 lg:px-8">
            <Hero :hero="hero" />

          <TwoColumnContent 
            :content="{
              title: '24/7 Emergency Water Damage Restoration',
              description: 'Fast response, professional cleanup, and complete restoration services for water damage emergencies. We work directly with your insurance company.',
              image: '/images/water-damage-restoration.jpg'
            }"
            backgroundColor="bg-[#F2F8FB]"
            imagePosition="left"
            :showDivider="false"
          />

        <div class="flex flex-col md:flex-row gap-8">
          <!-- Main Content -->
          <div class="w-full md:w-2/3 flex flex-col gap-8">
            


            <!-- Section with background and yellow header -->
            <section
              class="rounded-2xl overflow-hidden shadow-sm border border-[#fff4cc] bg-gradient-to-br from-[#fffef8] to-[#fffaed] hover:shadow-md transition-all duration-300 bg-gradient-to-br from-card/80 to-card/60 backdrop-blur-sm"
            >
              <!-- Yellow Header -->
              <div class="bg-gradient-to-r from-[#FFEE50] to-[#FFD700] text-gray-900 py-6 px-6 flex items-center justify-between">
                <div>
                  <h2 class="text-2xl font-bold tracking-tight">Why Choose Us?</h2>
                  <p class="text-sm opacity-90">Professional water damage restoration you can trust</p>
                </div>
                <Icon name="lucide:droplets" size="50" class="text-gray-900" />
              </div>

              <!-- Inner Content -->
              <div class="p-8">
                <Benefits :benefits="benefits"/>
                <div class="border-t border-[#d4ebff] my-8"></div>
                <InfoCards :info="info" />
              </div>
            </section>


            <CoverageFeatures :features="features" />
            <CTA :cta="cta" button-class="bg-gradient-to-r from-[#FFEE50] to-[#FFD700] py-6 px-6 text-gray-900 font-bold" />
            
            <!-- Emergency Contact Banner -->
            <div class="bg-red-600 text-white rounded-2xl p-8 text-center shadow-lg">
              <h3 class="text-3xl font-bold mb-2">🚨 Emergency? Call Now!</h3>
              <p class="text-xl mb-4">24/7 Response Team Available</p>
              <a href="tel:1-800-WATER-911" class="inline-block bg-white text-red-600 px-8 py-4 rounded-xl font-bold text-lg hover:bg-gray-100 transition-all">
                📞 1-800-WATER-911
              </a>
            </div>
          </div>

          <!-- Sidebar -->
          <div class="w-full md:w-1/3">
            <div class="bg-white rounded-2xl shadow-lg p-6 sticky top-6">
              <h3 class="text-2xl font-bold mb-4 text-gray-900">Get Free Estimate</h3>
              <div class="space-y-4 mb-6">
                <div class="flex items-center gap-3">
                  <Icon name="lucide:check-circle" class="text-green-600 w-6 h-6" />
                  <span class="text-gray-700">Fast 60-minute response</span>
                </div>
                <div class="flex items-center gap-3">
                  <Icon name="lucide:check-circle" class="text-green-600 w-6 h-6" />
                  <span class="text-gray-700">Insurance direct billing</span>
                </div>
                <div class="flex items-center gap-3">
                  <Icon name="lucide:check-circle" class="text-green-600 w-6 h-6" />
                  <span class="text-gray-700">Certified technicians</span>
                </div>
                <div class="flex items-center gap-3">
                  <Icon name="lucide:check-circle" class="text-green-600 w-6 h-6" />
                  <span class="text-gray-700">No hidden fees</span>
                </div>
              </div>
              <a href="/contact" class="block w-full bg-gradient-to-r from-[#FFEE50] to-[#FFD700] text-gray-900 text-center py-4 rounded-xl font-bold text-lg hover:shadow-lg transition-all">
                Request Free Estimate
              </a>
            </div>
          </div>
        </div>
        
        <!-- Trust Indicators -->
        <div class="mt-12 grid grid-cols-2 md:grid-cols-4 gap-6 text-center">
          <div class="bg-white p-6 rounded-xl shadow">
            <div class="text-4xl font-bold text-[#FFEE50] mb-2">24/7</div>
            <div class="text-sm text-gray-600">Emergency Response</div>
          </div>
          <div class="bg-white p-6 rounded-xl shadow">
            <div class="text-4xl font-bold text-[#FFEE50] mb-2">10k+</div>
            <div class="text-sm text-gray-600">Properties Restored</div>
          </div>
          <div class="bg-white p-6 rounded-xl shadow">
            <div class="text-4xl font-bold text-[#FFEE50] mb-2">98%</div>
            <div class="text-sm text-gray-600">Customer Satisfaction</div>
          </div>
          <div class="bg-white p-6 rounded-xl shadow">
            <div class="text-4xl font-bold text-[#FFEE50] mb-2">&lt;60min</div>
            <div class="text-sm text-gray-600">Average Response Time</div>
          </div>
        </div>
      </div>
    </main>
  </PatternSection>
</template>

<script setup>
// Enhanced SEO using stable composables
useEnhancedMetaTags()
useResourceHints(['/images/water-damage-restoration.jpg'])
usePerformanceMonitoring()

// Enhanced social sharing
useSocialMeta({
  title: '24/7 Emergency Water Damage Restoration | Fast Response',
  description: 'Professional water damage restoration services. Fast response, certified technicians, insurance direct billing. Call now for immediate assistance!',
  image: '/images/water-damage-restoration.jpg',
  url: 'https://www.amerusfinancial.com/ads/water-damage',
  type: 'website'
})

useSeoMeta({
  title: '24/7 Emergency Water Damage Restoration | Fast Response',
  ogTitle: 'Water Damage Restoration — Emergency Services Available',
  description:
    'Professional water damage restoration with 24/7 emergency response. Water extraction, drying, mold remediation. We work with your insurance. Call now!',
  ogDescription:
    'Professional water damage restoration with 24/7 emergency response. Water extraction, drying, mold remediation. We work with your insurance. Call now!',
  ogImage: '/images/water-damage-restoration.jpg',
  ogUrl: 'https://www.amerusfinancial.com/ads/water-damage',
  twitterCard: 'summary_large_image',
  twitterTitle: 'Water Damage Restoration — Emergency Services',
  twitterDescription:
    'Professional water damage restoration with 24/7 emergency response. Fast, reliable, and insurance approved. Call now for immediate help!',
  twitterImage: '/images/water-damage-restoration.jpg',
  keywords: 'water damage restoration, emergency water damage, flood cleanup, water extraction, water damage repair, burst pipe repair, mold remediation, 24/7 water damage, water damage company, water removal service'
})

// optional — add canonical link and enhanced meta tags
useHead({
  link: [
    {
      rel: 'canonical',
      href: 'https://www.amerusfinancial.com/ads/water-damage/'
    },
    // DNS prefetch for performance
    { rel: 'dns-prefetch', href: '//fonts.googleapis.com' },
    { rel: 'dns-prefetch', href: '//www.google-analytics.com' },
    // Preconnect for critical resources
    { rel: 'preconnect', href: 'https://fonts.gstatic.com', crossorigin: '' }
  ],
  meta: [
    // Enhanced crawling directives for ads
    { name: 'robots', content: 'noindex,nofollow' }, // Ad landing pages typically shouldn't be indexed
    // Social media optimization
    { name: 'twitter:site', content: '@waterdamagehelp' },
    { name: 'twitter:creator', content: '@waterdamagehelp' },
    // Technical SEO
    { name: 'format-detection', content: 'telephone=yes' }, // Enable phone number detection
    { name: 'theme-color', content: '#FFEE50' }
  ]
})

// Structured Data - Service Schema with consistent organization
const serviceProvider = useServiceProvider()

// Create review data
const reviewData = useReviewSchema([
  {
    author: 'Sarah Johnson',
    rating: 5,
    review: 'Called at 2am with a burst pipe emergency. They arrived in 45 minutes and had everything under control. Absolutely saved my home!',
    date: '2024-11-20'
  },
  {
    author: 'Michael Chen',
    rating: 5,
    review: 'Professional water damage restoration team. They handled everything including dealing with my insurance company. Highly recommend!',
    date: '2024-11-15'
  },
  {
    author: 'Lisa Rodriguez',
    rating: 5,
    review: 'Fast response, excellent communication, and thorough work. They restored my basement after flooding and it looks brand new.',
    date: '2024-11-10'
  }
])

// Create how-to steps
const howToSteps = useHowToSchema([
  {
    name: 'Call Emergency Line',
    text: 'Call our 24/7 emergency hotline immediately when you discover water damage. Our team is ready to respond within 60 minutes.',
    image: '/images/emergency-call.jpg'
  },
  {
    name: 'Initial Assessment',
    text: 'Our certified technicians arrive quickly to assess the damage, stop the water source, and begin emergency water extraction.',
    image: '/images/water-assessment.jpg'
  },
  {
    name: 'Restoration Process',
    text: 'We perform complete water removal, structural drying, dehumidification, and mold prevention using industrial equipment.',
    image: '/images/water-restoration.jpg'
  },
  {
    name: 'Final Restoration',
    text: 'Complete repairs and restoration of your property to pre-damage condition. We handle all insurance paperwork and coordination.',
    image: '/images/final-restoration.jpg'
  }
], 'How Water Damage Restoration Works', 'Professional water damage restoration process from emergency response to complete restoration.', 'PT2H', '2500.00')

useSchemaOrg([
  {
    '@type': 'Service',
    name: '24/7 Emergency Water Damage Restoration',
    provider: serviceProvider,
    description: 'Professional water damage restoration services with emergency response, water extraction, structural drying, mold remediation, and complete property restoration.',
    serviceType: 'Emergency Restoration Services',
    category: 'Water Damage Restoration',
    areaServed: {
      '@type': 'AdministrativeArea',
      name: 'United States'
    },
    availableChannel: {
      '@type': 'ServiceChannel',
      servicePhone: {
        '@type': 'ContactPoint',
        telephone: '+1-800-WATER-911',
        contactType: 'Emergency Services',
        availableLanguage: 'English',
        hoursAvailable: '24/7'
      }
    },
    offers: {
      '@type': 'Offer',
      price: '2500.00',
      priceCurrency: 'USD',
      description: 'Professional water damage restoration services - pricing varies by damage extent'
    }
  },
  
  // Review/Rating Schema for enhanced SERP display
  {
    '@type': 'LocalBusiness',
    name: 'Water Damage Restoration Services',
    description: 'Professional 24/7 emergency water damage restoration with certified technicians and insurance direct billing.',
    category: 'Water Damage Restoration',
    telephone: '+1-800-WATER-911',
    priceRange: '$$',
    ...reviewData
  },
  
  // FAQ Schema for better SERP features
  {
    '@type': 'FAQPage',
    mainEntity: [
      {
        '@type': 'Question',
        name: 'How quickly can you respond to water damage emergencies?',
        acceptedAnswer: {
          '@type': 'Answer',
          text: 'We provide 24/7 emergency response with an average arrival time of under 60 minutes. Our team is always ready to respond to water damage emergencies including burst pipes, floods, and leaks.'
        }
      },
      {
        '@type': 'Question',
        name: 'How much does water damage restoration cost?',
        acceptedAnswer: {
          '@type': 'Answer',
          text: 'Water damage restoration costs vary based on the extent of damage, affected area size, water category (clean, gray, or black water), and required services. We provide free estimates and work directly with insurance companies.'
        }
      },
      {
        '@type': 'Question',
        name: 'Do you work with insurance companies?',
        acceptedAnswer: {
          '@type': 'Answer',
          text: 'Yes, we work directly with all major insurance companies and handle the entire claims process. We provide detailed documentation, photos, and estimates to ensure your claim is processed smoothly.'
        }
      },
      {
        '@type': 'Question',
        name: 'What services are included in water damage restoration?',
        acceptedAnswer: {
          '@type': 'Answer',
          text: 'Our comprehensive water damage restoration includes emergency water extraction, structural drying, dehumidification, mold prevention and remediation, sanitization, odor removal, and complete repairs to restore your property to pre-damage condition.'
        }
      }
    ]
  },

  // HowTo Schema for application process
  howToSteps
])

const hero = {
  eyebrow: '24/7 Emergency Response',
  title: 'Water Damage? We Are Here to Help!',
  description: 'Professional water damage restoration services available 24/7. Fast response, certified technicians, and insurance approved. Call now for immediate assistance!',
  image: '/images/water-damage-emergency.jpg',
  imageAlt: 'emergency water damage restoration',
  cta: { href: 'tel:1-800-WATER-911', label: '📞 Call Now: 1-800-WATER-911' }
}
const benefits = [
  "⚡ Fastest response time - under 60 minutes average",
  "💰 Direct insurance billing - we handle all paperwork",
  "🏆 IICRC certified technicians with years of experience",
  "🛡️ Complete restoration - from extraction to repairs",
  "🔬 Advanced mold prevention and remediation",
  "✅ 100% satisfaction guarantee on all work"
]
const info = [
  {
    title: 'Response Time',
    text: 'Under 60 minutes',
    icon: 'lucide:clock'
  },
  {
    title: 'Availability',
    text: '24/7 Emergency Service',
    icon: 'lucide:phone'
  },
  {
    title: 'Coverage',
    text: 'All Insurance Accepted',
    icon: 'lucide:shield-check'
  }
]
const features = [
  '24/7 emergency water extraction and removal',
  'Advanced structural drying and dehumidification',
  'Mold inspection, prevention, and remediation',
  'Complete damage assessment and documentation',
  'Direct insurance company coordination',
  'Full property restoration to pre-damage condition'
]
const cta = {
  title: 'Do Not Wait - Water Damage Gets Worse Fast!',
  description: 'Every minute counts when dealing with water damage. Call our emergency response team now for immediate assistance.',
  primary: {
    href: 'tel:1-800-WATER-911',
    label: '📞 Call Emergency Line Now'
  }
}
</script>
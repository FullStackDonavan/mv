<template>
  <PatternSection>
    <main class="flex-grow">
      <div class="container mx-auto py-12 px-4 sm:px-6 lg:px-8">
            <Hero :hero="hero" />

          <TwoColumnContent 
            :content="{
              title: '24/7 Emergency Fire Damage Restoration',
              description: 'Fast response, professional cleanup, and complete restoration services for fire and smoke damage emergencies. We work directly with your insurance company.',
              image: '/images/fire-damage-restoration.jpg'
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
                  <p class="text-sm opacity-90">Professional fire damage restoration you can trust</p>
                </div>
                <Icon name="lucide:flame" size="50" class="text-gray-900" />
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
              <h3 class="text-3xl font-bold mb-2">� Fire Emergency? Call Now!</h3>
              <p class="text-xl mb-4">24/7 Fire Restoration Team Available</p>
              <a href="tel:1-800-FIRE-911" class="inline-block bg-white text-red-600 px-8 py-4 rounded-xl font-bold text-lg hover:bg-gray-100 transition-all">
                📞 1-800-FIRE-911
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
useResourceHints(['/images/fire-damage-restoration.jpg'])
usePerformanceMonitoring()

// Enhanced social sharing
useSocialMeta({
  title: '24/7 Emergency Fire Damage Restoration | Fast Response',
  description: 'Professional fire damage restoration services. Fast response, certified technicians, insurance direct billing. Call now for immediate assistance!',
  image: '/images/fire-damage-restoration.jpg',
  url: 'https://www.amerusfinancial.com/ads/fire-damage',
  type: 'website'
})

useSeoMeta({
  title: '24/7 Emergency Fire Damage Restoration | Fast Response',
  ogTitle: 'Fire Damage Restoration — Emergency Services Available',
  description:
    'Professional fire damage restoration with 24/7 emergency response. Smoke cleanup, soot removal, odor elimination. We work with your insurance. Call now!',
  ogDescription:
    'Professional fire damage restoration with 24/7 emergency response. Smoke cleanup, soot removal, odor elimination. We work with your insurance. Call now!',
  ogImage: '/images/fire-damage-restoration.jpg',
  ogUrl: 'https://www.amerusfinancial.com/ads/fire-damage',
  twitterCard: 'summary_large_image',
  twitterTitle: 'Fire Damage Restoration — Emergency Services',
  twitterDescription:
    'Professional fire damage restoration with 24/7 emergency response. Fast, reliable, and insurance approved. Call now for immediate help!',
  twitterImage: '/images/fire-damage-restoration.jpg',
  keywords: 'fire damage restoration, emergency fire damage, smoke cleanup, soot removal, fire restoration, smoke damage repair, odor removal, 24/7 fire damage, fire damage company, fire restoration service'
})

// optional — add canonical link and enhanced meta tags
useHead({
  link: [
    {
      rel: 'canonical',
      href: 'https://www.amerusfinancial.com/ads/fire-damage/'
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
    { name: 'twitter:site', content: '@firedamagehelp' },
    { name: 'twitter:creator', content: '@firedamagehelp' },
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
    review: 'After a kitchen fire, they responded immediately and handled everything from smoke cleanup to full restoration. They saved our home!',
    date: '2024-11-20'
  },
  {
    author: 'Michael Chen',
    rating: 5,
    review: 'Professional fire damage restoration team. They removed all smoke odor and soot damage. Dealt with insurance directly. Highly recommend!',
    date: '2024-11-15'
  },
  {
    author: 'Lisa Rodriguez',
    rating: 5,
    review: 'Fast response after electrical fire. Excellent communication and thorough work. They restored our living room perfectly - no trace of damage.',
    date: '2024-11-10'
  }
])

// Create how-to steps
const howToSteps = useHowToSchema([
  {
    name: 'Call Emergency Line',
    text: 'Call our 24/7 emergency hotline immediately after fire damage. Our team is ready to respond within 60 minutes to secure your property.',
    image: '/images/emergency-call.jpg'
  },
  {
    name: 'Initial Assessment',
    text: 'Our certified technicians arrive quickly to assess fire, smoke, and soot damage. We secure the property and begin emergency board-up if needed.',
    image: '/images/fire-assessment.jpg'
  },
  {
    name: 'Restoration Process',
    text: 'We perform complete smoke and soot removal, odor elimination, structural cleaning, and air purification using specialized equipment.',
    image: '/images/fire-restoration.jpg'
  },
  {
    name: 'Final Restoration',
    text: 'Complete repairs and restoration of your property to pre-fire condition. We handle all insurance paperwork and coordination.',
    image: '/images/final-restoration.jpg'
  }
], 'How Fire Damage Restoration Works', 'Professional fire damage restoration process from emergency response to complete restoration.', 'PT3H', '3500.00')

useSchemaOrg([
  {
    '@type': 'Service',
    name: '24/7 Emergency Fire Damage Restoration',
    provider: serviceProvider,
    description: 'Professional fire damage restoration services with emergency response, smoke cleanup, soot removal, odor elimination, and complete property restoration.',
    serviceType: 'Emergency Restoration Services',
    category: 'Fire Damage Restoration',
    areaServed: {
      '@type': 'AdministrativeArea',
      name: 'United States'
    },
    availableChannel: {
      '@type': 'ServiceChannel',
      servicePhone: {
        '@type': 'ContactPoint',
        telephone: '+1-800-FIRE-911',
        contactType: 'Emergency Services',
        availableLanguage: 'English',
        hoursAvailable: '24/7'
      }
    },
    offers: {
      '@type': 'Offer',
      price: '3500.00',
      priceCurrency: 'USD',
      description: 'Professional fire damage restoration services - pricing varies by damage extent'
    }
  },
  
  // Review/Rating Schema for enhanced SERP display
  {
    '@type': 'LocalBusiness',
    name: 'Fire Damage Restoration Services',
    description: 'Professional 24/7 emergency fire damage restoration with certified technicians and insurance direct billing.',
    category: 'Fire Damage Restoration',
    telephone: '+1-800-FIRE-911',
    priceRange: '$$$',
    ...reviewData
  },
  
  // FAQ Schema for better SERP features
  {
    '@type': 'FAQPage',
    mainEntity: [
      {
        '@type': 'Question',
        name: 'How quickly can you respond to fire damage emergencies?',
        acceptedAnswer: {
          '@type': 'Answer',
          text: 'We provide 24/7 emergency response with an average arrival time of under 60 minutes. Our team is always ready to respond to fire damage emergencies including house fires, kitchen fires, and electrical fires.'
        }
      },
      {
        '@type': 'Question',
        name: 'How much does fire damage restoration cost?',
        acceptedAnswer: {
          '@type': 'Answer',
          text: 'Fire damage restoration costs vary based on the extent of fire, smoke, and soot damage, affected area size, structural damage, and required services. We provide free estimates and work directly with insurance companies.'
        }
      },
      {
        '@type': 'Question',
        name: 'Do you work with insurance companies?',
        acceptedAnswer: {
          '@type': 'Answer',
          text: 'Yes, we work directly with all major insurance companies and handle the entire claims process. We provide detailed documentation, photos, and estimates to ensure your fire claim is processed smoothly.'
        }
      },
      {
        '@type': 'Question',
        name: 'What services are included in fire damage restoration?',
        acceptedAnswer: {
          '@type': 'Answer',
          text: 'Our comprehensive fire damage restoration includes emergency board-up, smoke and soot removal, odor elimination, structural cleaning, air purification, content restoration, and complete repairs to restore your property to pre-fire condition.'
        }
      }
    ]
  },

  // HowTo Schema for application process
  howToSteps
])

const hero = {
  eyebrow: '24/7 Emergency Response',
  title: 'Fire Damage? We Are Here to Help!',
  description: 'Professional fire damage restoration services available 24/7. Fast response, certified technicians, and insurance approved. Call now for immediate assistance!',
  image: '/images/fire-damage-emergency.jpg',
  imageAlt: 'emergency fire damage restoration',
  cta: { href: 'tel:1-800-FIRE-911', label: '📞 Call Now: 1-800-FIRE-911' }
}
const benefits = [
  "⚡ Fastest response time - under 60 minutes average",
  "💰 Direct insurance billing - we handle all paperwork",
  "🏆 IICRC certified fire restoration technicians",
  "🛡️ Complete restoration - from cleanup to repairs",
  "🔬 Advanced smoke odor elimination technology",
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
  '24/7 emergency fire damage response and board-up',
  'Advanced smoke and soot removal techniques',
  'Complete odor elimination and air purification',
  'Detailed damage assessment and documentation',
  'Direct insurance company coordination',
  'Full property restoration to pre-fire condition'
]
const cta = {
  title: 'Do Not Wait - Fire Damage Gets Worse Fast!',
  description: 'Every minute counts when dealing with fire damage. Call our emergency response team now for immediate assistance.',
  primary: {
    href: 'tel:1-800-FIRE-911',
    label: '📞 Call Emergency Line Now'
  }
}
</script>
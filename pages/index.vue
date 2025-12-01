<template>
  <PatternSection class="py-16 bg-gray-50">
    <HomepageHeroSection />
    <div class="container mx-auto px-4 max-w-7xl">
      <ContentList path="/articles" v-slot="{ list }">
        <div class="flex flex-col items-center">
          <h1 class="text-4xl md:text-5xl font-bold text-center mb-4 text-gray-900 dark:text-white">Water & Fire Damage Restoration Resources</h1>
          <p class="text-lg text-gray-600 dark:text-gray-300 text-center mb-12 max-w-3xl">
            Expert guidance on emergency response, damage restoration, and protecting your property from water and fire disasters.
          </p>
          
          <!-- Articles Grid -->
          <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-8 w-full">
            <article
              v-for="article in list"
              :key="article._path"
              class="bg-white dark:bg-gray-800 rounded-2xl overflow-hidden shadow-lg hover:shadow-2xl transition-all duration-300 hover:-translate-y-2 flex flex-col"
            >
              <NuxtLink :to="article._path" class="flex flex-col h-full">
                <!-- Article Image -->
                <div v-if="article.img" class="relative h-48 overflow-hidden bg-gray-200">
                  <NuxtImg 
                    :src="article.img"
                    :alt="article.title"
                    format="webp"
                    class="w-full h-full object-cover transition-transform duration-300 hover:scale-110"
                    sizes="sm:100vw md:50vw lg:33vw"
                    quality="80"
                    loading="lazy"
                  />
                </div>
                
                <!-- Article Content -->
                <div class="p-6 flex flex-col flex-grow">
                  <!-- Category Badge (if available) -->
                  <div v-if="article.subject" class="mb-3">
                    <span class="inline-flex items-center rounded-full border px-3 py-1 text-xs font-semibold bg-blue-50 text-blue-700 border-blue-200 dark:bg-blue-900/30 dark:text-blue-300 dark:border-blue-800">
                      {{ article.subject }}
                    </span>
                  </div>
                  
                  <!-- Article Title -->
                  <h2 class="text-xl font-bold mb-3 text-gray-900 dark:text-white line-clamp-2 hover:text-blue-600 dark:hover:text-blue-400 transition-colors">
                    {{ article.title }}
                  </h2>
                  
                  <!-- Article Description -->
                  <p class="text-gray-600 dark:text-gray-300 text-sm mb-4 line-clamp-3 flex-grow">
                    {{ article.description }}
                  </p>
                  
                  <!-- Article Meta -->
                  <div class="flex items-center justify-between text-xs text-gray-500 dark:text-gray-400 pt-4 border-t border-gray-200 dark:border-gray-700">
                    <span v-if="article.author" class="flex items-center gap-1">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                      </svg>
                      {{ article.author }}
                    </span>
                    <span v-if="article.date" class="flex items-center gap-1">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
                      </svg>
                      {{ article.date }}
                    </span>
                  </div>
                  
                  <!-- Read More Arrow -->
                  <div class="flex items-center gap-2 text-blue-600 dark:text-blue-400 font-semibold text-sm mt-4 group">
                    <span>Read Article</span>
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 transition-transform group-hover:translate-x-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                    </svg>
                  </div>
                </div>
              </NuxtLink>
            </article>
          </div>
        </div>
      </ContentList>
    </div>
  </PatternSection>
</template>

<script setup lang="ts">
// Enhanced SEO using stable composables
useEnhancedMetaTags()
useResourceHints(['/images/contact-og.jpg'])
usePerformanceMonitoring()

// Consolidated SEO + Social Meta for Home page (now showing articles)
const pageUrl = 'https://www.amerusfinancial.com/'
const pageTitle = 'Water & Fire Damage Restoration | Emergency Response & Recovery'
const pageDescription = 'Professional water and fire damage restoration services. Expert emergency response, cleanup, and recovery solutions. Available 24/7 for residential and commercial properties.'
const pageImage = '/images/amerus-og-default.jpg'

useHead({
  title: pageTitle,
  meta: [
    // Basic meta
    { name: 'description', content: pageDescription },

    // Required Open Graph tags
    { property: 'og:type', content: 'website' },
    { property: 'og:locale', content: 'en_US' },
    { property: 'og:site_name', content: 'Amerus Financial' },
    { property: 'og:title', content: pageTitle },
    { property: 'og:description', content: pageDescription },
    { property: 'og:image', content: pageImage },
    { property: 'og:url', content: pageUrl },

    // Twitter Card
    { name: 'twitter:card', content: 'summary_large_image' },
    { name: 'twitter:title', content: pageTitle },
    { name: 'twitter:description', content: pageDescription },
    { name: 'twitter:image', content: pageImage },
    { name: 'twitter:site', content: '@amerusfinancial' },
    { name: 'twitter:creator', content: '@amerusfinancial' },

    // Technical SEO
    { name: 'robots', content: 'index,follow,max-image-preview:large,max-snippet:-1,max-video-preview:-1' },
    { name: 'googlebot', content: 'index,follow,max-image-preview:large,max-snippet:-1,max-video-preview:-1' }
  ],
  link: [
    { rel: 'canonical', href: pageUrl },
    // Performance optimizations
    { rel: 'dns-prefetch', href: '//fonts.googleapis.com' },
    { rel: 'dns-prefetch', href: '//www.google-analytics.com' },
    { rel: 'preconnect', href: 'https://fonts.gstatic.com', crossorigin: '' }
  ]
})

// Structured Data - Home WebPage schema + Organization reference
const organization = useServiceProvider()
useSchemaOrg([
  // Primary image for the Articles overview page with extended licensing / attribution metadata
  {
    '@type': 'ImageObject',
    '@id': pageUrl + '#primaryimage',
    url: pageImage,
    contentUrl: pageImage,
    caption: pageTitle,
    // Creator can be an Organization (your company) or a Person
    creator: {
      '@type': 'Organization',
      name: 'Amerus Financial',
      url: 'https://www.amerusfinancial.com'
    },
    creditText: 'Amerus Financial',
    copyrightNotice: `Copyright ${new Date().getFullYear()} Amerus Financial. All rights reserved.`,
    acquireLicensePage: 'https://www.amerusfinancial.com/about-us'
  },
  {
    '@type': 'WebPage',
    '@id': pageUrl,
    url: pageUrl,
    name: pageTitle,
    description: pageDescription,
    primaryImageOfPage: { '@id': pageUrl + '#primaryimage' },
    isPartOf: {
      '@type': 'Website',
      name: 'Amerus Financial',
      url: 'https://www.amerusfinancial.com'
    },
    about: organization,
    breadcrumb: {
      '@type': 'BreadcrumbList',
      itemListElement: [
        { '@type': 'ListItem', position: 1, name: 'Home', item: 'https://www.amerusfinancial.com/' },
        { '@type': 'ListItem', position: 2, name: 'Resources', item: pageUrl }
      ]
    }
  }
])
</script>


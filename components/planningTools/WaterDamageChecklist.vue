<template>
    <section class="bg-white" aria-labelledby="water-damage-checklist">
  <div class="flex flex-col gap-8">

    <!-- Container for remaining content -->
    <div class="container mx-auto px-4 pb-12">
            <!-- Header Section -->
    <div class="mb-6 animate-fade-in-up">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-center">
        <!-- Left Column: Text Content -->
        <div class="text-center md:text-left">
          <h1 class="text-3xl md:text-4xl font-bold mb-4 text-gray-900">Water Damage Response Checklist</h1>
          <p class="text-lg text-gray-600 max-w-3xl mx-auto md:mx-0 mb-6">
            Act quickly to minimize damage and protect your property. Follow this step-by-step checklist 
            based on common water damage scenarios to ensure proper response and recovery.
          </p>
          <!-- Feature Tags -->
          <div class="flex flex-wrap justify-center md:justify-start gap-3 mb-6">
            <div class="inline-flex items-center rounded-full border px-2.5 py-0.5 font-semibold transition-colors text-sm bg-blue-50 text-blue-600 border-blue-200">
              Scenario-Based Guidance
            </div>
            <div class="inline-flex items-center rounded-full border px-2.5 py-0.5 font-semibold transition-colors text-sm bg-green-50 text-green-600 border-green-200">
              Interactive Progress Tracking
            </div>
            <div class="inline-flex items-center rounded-full border px-2.5 py-0.5 font-semibold transition-colors text-sm bg-purple-50 text-purple-600 border-purple-200">
              Emergency Ready
            </div>
            <div class="inline-flex items-center rounded-full border px-2.5 py-0.5 font-semibold transition-colors text-sm bg-amber-50 text-amber-600 border-amber-200">
              Expert Tips
            </div>
          </div>
          <!-- Download Button -->
          <div class="flex justify-center md:justify-start gap-4 mt-4">
            <button 
              @click="downloadPDF"
              class="inline-flex items-center gap-2 px-4 py-2 rounded-xl border border-gray-300 bg-white hover:bg-gray-50 transition-all duration-300 hover:shadow-md"
            >
              <Icon name="lucide-download" class="h-4 w-4" />
              <span>Save as PDF</span>
            </button>
          </div>
        </div>
        <!-- Right Column: Nuxt Image -->
        <div class="flex justify-center md:justify-end">
          <NuxtImg src="/images/water-damage-response.jpg" alt="Water Damage Response Illustration" class="rounded-2xl shadow-lg object-cover" />
        </div>
      </div>
    </div>
        <!-- How to Use Alert -->
        <div class="bg-red-50 border border-red-200 rounded-xl p-6 mb-4 animate-fade-in-up animation-delay-200">
        <div class="flex gap-4">
            <Icon name="lucide-alert-triangle" class="h-5 w-5 text-red-600 flex-shrink-0 mt-0.5" />
            <div>
            <h5 class="mb-2 font-semibold text-red-900">Safety First</h5>
            <div class="text-sm text-red-800 space-y-2">
                <p><strong>If you experience water damage:</strong> Ensure your safety first. Turn off electricity in affected areas if safe to do so. If there's any doubt about safety, evacuate and call professionals.</p>
                <p>Check off items as you complete them to track your progress. Your checklist is saved automatically in your browser.</p>
            </div>
            </div>
        </div>
        </div>

        <!-- Progress Overview Card -->
        <div class="bg-white rounded-2xl shadow-xl border border-gray-100 mb-8 animate-fade-in-up animation-delay-400">
        <!-- Card Header -->
        <div class="bg-gradient-to-r from-[#FFEE50] to-[#FFD700] py-6 px-8 rounded-t-2xl">
            <div class="flex justify-between items-center">
            <div>
                <h3 class="text-2xl font-semibold text-gray-900">Your Response Progress</h3>
                <p class="text-gray-700 text-sm mt-1">Overall progress across all scenarios</p>
            </div>
            <button 
                @click="resetProgress"
                class="inline-flex items-center gap-2 px-3 py-2 rounded-xl bg-gray-900/10 hover:bg-gray-900/20 transition-colors duration-300 text-gray-900 text-sm font-medium"
            >
                <Icon name="lucide-square" class="h-3 w-3" />
                Reset Progress
            </button>
            </div>
        </div>

        <!-- Progress Content -->
        <div class="p-8 bg-gradient-to-br from-gray-50 to-white rounded-b-2xl">
            <div class="space-y-6">
            <!-- Overall Progress -->
            <div>
                <div class="flex justify-between mb-2">
                <span class="text-sm font-semibold text-gray-700">Overall Progress</span>
                <span class="text-sm font-semibold text-gray-900">{{ overallProgress }}%</span>
                </div>
                <div class="w-full bg-gray-200 rounded-full h-3">
                <div 
                    class="bg-gradient-to-r from-[#FFEE50] to-[#FFD700] h-3 rounded-full transition-all duration-700 ease-out"
                    :style="{ width: `${overallProgress}%` }"
                ></div>
                </div>
            </div>

            <!-- Scenario Progress -->
            <div class="grid grid-cols-1 md:grid-cols-5 gap-4">
                <div v-for="(scenario, key) in scenarios" :key="key">
                <div class="flex justify-between mb-1">
                    <span class="text-xs font-medium text-gray-600">{{ scenario.label }}</span>
                    <span class="text-xs text-gray-900">{{ getScenarioProgress(key) }}%</span>
                </div>
                <div class="w-full bg-gray-200 rounded-full h-2">
                    <div 
                    class="bg-gradient-to-r from-[#FFEE50] to-[#FFD700] h-2 rounded-full transition-all duration-500"
                    :style="{ width: `${getScenarioProgress(key)}%` }"
                    ></div>
                </div>
                </div>
            </div>
            </div>
        </div>
        </div>

        <!-- Tabs Navigation -->
        <div class="bg-white rounded-xl p-2 shadow-lg border-2 border-gray-200 mb-6">
        <div class="rounded-xl p-1 grid grid-cols-2 md:grid-cols-6 gap-1">
            <button 
            v-for="(scenario, key) in scenarios"
            :key="key"
            @click="activeTab = key"
            class="px-4 py-3 rounded-lg text-sm font-semibold transition-all duration-300 focus:outline-none focus:ring-4 focus:ring-[#FFEE50]/20"
            :class="activeTab === key 
              ? 'bg-gradient-to-r from-[#FFEE50] to-[#FFD700] text-gray-900 shadow-lg transform scale-105' 
              : 'text-gray-600 hover:text-gray-900 hover:bg-gray-50'"
          >
          {{ scenario.label }}
            </button>
        </div>
        </div>

        <!-- Tab Content -->
        <div class="animate-fade-in-up animation-delay-800">
        <!-- Show content for active tab only -->
        <div class="bg-white rounded-2xl shadow-xl border border-gray-100">
            <!-- Tab Header -->
            <div class="bg-gradient-to-r from-[#FFEE50] to-[#FFD700] py-6 px-8 rounded-t-2xl">
              <div class="flex flex-col md:flex-row md:items-center md:justify-between gap-4">
                <div>
                  <h3 class="text-xl font-semibold text-gray-900">{{ scenarios[activeTab]?.title }}</h3>
                  <p class="text-gray-700 text-sm mt-1">{{ scenarios[activeTab]?.description }}</p>
                </div>
                <!-- Search Bar Floated Right -->
                <div class="w-full md:w-auto">
                  <div class="relative max-w-md md:max-w-xs ml-auto animate-fade-in-up animation-delay-700">
                    <Icon name="lucide-search" class="absolute left-3 top-1/2 transform -translate-y-1/2 h-4 w-4 text-gray-600" />
                    <input
                      v-model="searchQuery"
                      type="text"
                      placeholder="Search checklist items..."
                      class="w-full pl-10 pr-4 py-2 border border-gray-300 rounded-xl bg-white text-gray-900 placeholder-gray-500 focus:ring-2 focus:ring-[#FFEE50] focus:border-[#FFEE50] transition-all duration-300"
                    />
                    <button 
                      v-if="searchQuery"
                      @click="searchQuery = ''"
                      class="absolute right-3 top-1/2 transform -translate-y-1/2 text-gray-500 hover:text-gray-700 transition-colors duration-200"
                    >
                      <Icon name="lucide-x" class="h-4 w-4" />
                    </button>
                  </div>
                </div>
              </div>
            </div>

            <!-- Checklist Content -->
            <div class="p-8 bg-gradient-to-br from-gray-50 to-white rounded-b-2xl">
            <div v-for="(category, categoryKey) in checklistData" :key="categoryKey" class="mb-8 last:mb-0">
                <!-- Only show category if it has items for this scenario -->
                <template v-if="getFilteredItems(categoryKey, activeTab).length > 0">
                <div class="flex items-center justify-between mb-6">
                    <div class="flex items-center gap-3">
                    <Icon :name="category.icon" :class="`h-16 w-16 ${category.color}`" />
                    <div>
                        <h3 class="text-lg font-semibold text-gray-900">{{ category.title }}</h3>
                        <p class="text-sm text-gray-500">{{ getCategoryProgress(categoryKey, activeTab) }}% complete</p>
                    </div>
                    </div>
                    <!-- Category progress bar -->
                    <div class="w-24 h-2 bg-gray-200 rounded-full overflow-hidden">
                    <div 
                        class="h-full bg-gradient-to-r from-[#FFEE50] to-[#FFD700] transition-all duration-500 ease-out"
                        :style="`width: ${getCategoryProgress(categoryKey, activeTab)}%`"
                    ></div>
                    </div>
                </div>

                <div class="space-y-4 pl-4 border-l-2 border-gray-200">
                    <div 
                    v-for="item in getFilteredItems(categoryKey, activeTab)"
                    :key="item.id"
                    class="flex items-start gap-4 py-2 group hover:bg-blue-50/50 rounded-lg px-3 -mx-3 transition-colors duration-300"
                    >
                    <div class="flex-none pt-1">
                        <button
                        @click="toggleItem(item.id)"
                        :data-item-id="item.id"
                        :class="[
                            'relative h-5 w-5 rounded-md border-2 transition-all duration-300 focus:outline-none focus:ring-2 focus:ring-[#FFEE50] focus:ring-offset-2 flex items-center justify-center',
                            completedItems.has(item.id)
                            ? 'bg-gradient-to-r from-[#FFEE50] to-[#FFD700] border-[#FFEE50] text-gray-900 shadow-md transform scale-105'
                            : 'border-gray-300 hover:border-[#FFEE50] hover:bg-yellow-50 bg-white shadow-sm'
                        ]"
                        >
                        <Icon 
                            v-if="completedItems.has(item.id)" 
                            name="lucide-check" 
                            class="h-4 w-4 drop-shadow-sm" 
                        />
                        <!-- Unchecked state indicator -->
                        <div 
                            v-else
                            class="w-2 h-2 rounded-full bg-gray-200 opacity-0 group-hover:opacity-100 transition-opacity duration-300"
                        ></div>
                        </button>
                    </div>
                    <div class="flex-1">
                        <label 
                        :class="[
                            'text-sm font-medium cursor-pointer transition-all duration-300',
                            completedItems.has(item.id) 
                            ? 'line-through text-gray-500' 
                            : 'text-gray-900 group-hover:text-gray-700'
                        ]"
                        @click="toggleItem(item.id)"
                        >
                        {{ item.title }}
                        <span 
                            :class="[
                            'ml-2 inline-flex items-center rounded-full border px-2 py-0.5 text-xs font-medium',
                            getScenarioStyle(item.scenario)
                            ]"
                        >
                            {{ scenarios[item.scenario]?.label }}
                        </span>
                        </label>
                        
                        <!-- Expert Tip Toggle Button -->
                        <button 
                        @click="toggleExpertTip(item.id)"
                        :class="[
                            'mt-2 inline-flex items-center gap-1 text-xs font-medium px-2 py-1 rounded-full transition-all duration-300',
                            visibleExpertTips.has(item.id)
                            ? 'bg-amber-100 text-amber-800 hover:bg-amber-200'
                            : 'bg-gray-100 text-gray-600 hover:bg-gray-200'
                        ]"
                        >
                        <Icon name="lucide-lightbulb" class="h-3 w-3" />
                        <span>{{ visibleExpertTips.has(item.id) ? 'Hide' : 'Show' }} Expert Tip</span>
                        </button>
                        
                        <!-- Animated Expert Tip Content -->
                        <transition 
                        enter-active-class="transition-all duration-300 ease-out" 
                        enter-from-class="opacity-0 -translate-y-2 max-h-0" 
                        enter-to-class="opacity-100 translate-y-0 max-h-96"
                        leave-active-class="transition-all duration-200 ease-in" 
                        leave-from-class="opacity-100 translate-y-0 max-h-96" 
                        leave-to-class="opacity-0 -translate-y-2 max-h-0"
                        >
                        <div v-if="visibleExpertTips.has(item.id)" class="mt-3 bg-gradient-to-r from-amber-50 to-orange-50 border-l-4 border-amber-400 p-3 rounded-r-lg overflow-hidden">
                            <div class="flex items-start gap-2">
                            <Icon name="lucide-lightbulb" class="h-4 w-4 text-amber-600 mt-0.5 flex-shrink-0" />
                            <div>
                                <p class="text-xs font-semibold text-amber-800 uppercase tracking-wide mb-1">Expert Tip</p>
                                <p class="text-sm text-amber-700">{{ item.description }}</p>
                            </div>
                            </div>
                        </div>
                        </transition>
                    </div>
                    </div>
                </div>
                </template>
            </div>
            </div>
        </div>
        
        <!-- CTA Section -->
        <div class="bg-gradient-to-r from-blue-50 to-blue-100 border border-blue-200 rounded-2xl p-8 mt-8 animate-fade-in-up animation-delay-1000">
        <div class="flex flex-col md:flex-row gap-6 items-center">
            <div class="flex-1 text-center md:text-left">
            <h3 class="text-xl font-semibold text-gray-900 mb-2">Need Professional Water Damage Restoration?</h3>
            <p class="text-gray-600 mb-4">
                Our certified water damage restoration specialists are available 24/7 to respond to emergencies and help you recover from water damage quickly and safely.
            </p>
            <NuxtLink 
                to="/contact"
                class="inline-flex items-center gap-2 bg-gradient-to-r from-[#FFEE50] to-[#FFD700] text-gray-900 px-6 py-3 rounded-xl hover:shadow-lg transition-all duration-300 transform hover:scale-105 font-semibold"
            >
                <Icon name="lucide-phone" class="h-4 w-4" />
                <span>Call for Emergency Service</span>
            </NuxtLink>
            </div>
            
            <div class="flex-none">
            <div class="bg-white/70 rounded-xl p-4 flex gap-6 text-center">
                <div class="flex flex-col items-center">
                <Icon name="lucide-clock" class="h-8 w-8 mb-2 text-gray-900" />
                <p class="text-sm font-medium text-gray-700">24/7<br>Response</p>
                </div>
                <div class="flex flex-col items-center">
                <Icon name="lucide-shield-check" class="h-8 w-8 mb-2 text-gray-900" />
                <p class="text-sm font-medium text-gray-700">Certified<br>Experts</p>
                </div>
                <div class="flex flex-col items-center">
                <Icon name="lucide-check-circle" class="h-8 w-8 mb-2 text-gray-900" />
                <p class="text-sm font-medium text-gray-700">Insurance<br>Assistance</p>
                </div>
            </div>
            </div>
        </div>
        </div>
        </div>
    </div>
    <!-- End container -->
  </div>
  </section>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'

// Types
interface ChecklistItem {
  id: string
  title: string
  description: string
  scenario: string
}

interface Category {
  title: string
  icon: string
  color: string
  items: ChecklistItem[]
}

interface Scenario {
  label: string
  title: string
  description: string
}

// Reactive data
const activeTab = ref('all')
const completedItems = ref(new Set<string>())
const visibleExpertTips = ref(new Set<string>())
const searchQuery = ref('')

// Scenario configuration
const scenarios: Record<string, Scenario> = {
  all: { label: 'All Scenarios', title: 'Complete Water Damage Response Checklist', description: 'All items across all water damage scenarios.' },
  'burst-pipe': { label: 'Burst Pipe', title: 'Burst Pipe Response', description: 'Immediate steps for plumbing failures and burst pipes.' },
  'flood': { label: 'Flood', title: 'Flood Damage Response', description: 'Critical actions for natural flooding events.' },
  'appliance': { label: 'Appliance Leak', title: 'Appliance Leak Response', description: 'Steps for washer, dishwasher, and water heater leaks.' },
  'roof': { label: 'Roof Leak', title: 'Roof Leak Response', description: 'Actions for storm damage and roof leaks.' },
  'sewage': { label: 'Sewage Backup', title: 'Sewage Backup Response', description: 'Emergency procedures for sewage and black water issues.' }
}

// Checklist data structure
const checklistData: Record<string, Category> = {
  immediate: {
    title: 'Immediate Safety Actions',
    icon: 'lucide-alert-triangle',
    color: 'text-red-500',
    items: [
      { id: '1-1', title: 'Ensure everyone\'s safety - evacuate if necessary', description: 'If there\'s any danger from electrical hazards, structural damage, or contaminated water, evacuate immediately and call 911. Your safety is more important than property.', scenario: 'all' },
      { id: '1-2', title: 'Turn off electricity to affected areas (if safe to do so)', description: 'Water and electricity are a deadly combination. If you can safely reach your circuit breaker without walking through water, shut off power to affected areas. If unsure, call an electrician.', scenario: 'all' },
      { id: '1-3', title: 'Shut off the main water supply', description: 'Locate your main water shutoff valve (usually near the water meter or where the main line enters your home) and turn it off to stop additional water flow.', scenario: 'burst-pipe' },
      { id: '1-4', title: 'Turn off the water supply to the leaking appliance', description: 'Most appliances have a dedicated shutoff valve nearby. Turn it clockwise to stop the water flow. If you can\'t find it, shut off the main water supply.', scenario: 'appliance' },
      { id: '1-5', title: 'Do NOT enter flooded areas with standing water', description: 'Floodwater can hide hazards like sharp objects, electrical dangers, and contamination. Wait for professional clearance before entering.', scenario: 'flood' },
      { id: '1-6', title: 'Avoid contact with sewage water - evacuate affected areas', description: 'Sewage contains dangerous bacteria, viruses, and pathogens. Do not attempt to clean it yourself. Call professional sewage cleanup services immediately.', scenario: 'sewage' },
      { id: '1-7', title: 'Place buckets or containers under active leaks', description: 'Temporarily contain dripping water with buckets, plastic containers, or tarps to prevent additional damage while you arrange repairs.', scenario: 'roof' }
    ]
  },
  documentation: {
    title: 'Documentation & Insurance',
    icon: 'lucide-camera',
    color: 'text-blue-500',
    items: [
      { id: '2-1', title: 'Take photos and videos of all damage before cleanup', description: 'Document everything from multiple angles. Include close-ups of damaged items and wide shots showing the extent. This documentation is crucial for insurance claims.', scenario: 'all' },
      { id: '2-2', title: 'Document water source and cause of damage', description: 'Take photos showing where the water came from (burst pipe, leak, etc.). This helps establish the cause for your insurance claim.', scenario: 'all' },
      { id: '2-3', title: 'Make a detailed inventory of damaged items', description: 'List all affected items with descriptions, approximate age, and original cost if possible. Include receipts or purchase records if available.', scenario: 'all' },
      { id: '2-4', title: 'Contact your insurance company immediately', description: 'Report the loss within 24-48 hours. Many policies require prompt notification. Ask about immediate steps and whether they\'ll send an adjuster.', scenario: 'all' },
      { id: '2-5', title: 'Keep all receipts for emergency repairs and cleanup', description: 'Save receipts for tarps, fans, cleaning supplies, hotel stays, and professional services. These may be reimbursable under your policy.', scenario: 'all' },
      { id: '2-6', title: 'Do not dispose of damaged items until adjuster approves', description: 'The insurance adjuster needs to see damaged items to verify your claim. Get written permission before discarding anything.', scenario: 'all' }
    ]
  },
  waterRemoval: {
    title: 'Water Removal & Drying',
    icon: 'lucide-droplet',
    color: 'text-cyan-500',
    items: [
      { id: '3-1', title: 'Remove standing water with pumps, wet vacs, or mops', description: 'The faster you remove water, the less damage occurs. For minor leaks, use towels and mops. For significant water, rent a wet vacuum or submersible pump.', scenario: 'all' },
      { id: '3-2', title: 'Move furniture and belongings to dry areas', description: 'Remove or elevate furniture, rugs, and belongings from wet areas. Place aluminum foil or wood blocks under furniture legs to prevent further moisture damage.', scenario: 'all' },
      { id: '3-3', title: 'Set up fans and dehumidifiers for air circulation', description: 'Proper airflow is critical for drying. Position fans to create cross-ventilation. Run dehumidifiers continuously and empty them regularly.', scenario: 'all' },
      { id: '3-4', title: 'Open windows and doors (if weather permits) for ventilation', description: 'If outside humidity is lower than inside, opening windows helps. However, close them if it\'s raining or very humid outside.', scenario: 'all' },
      { id: '3-5', title: 'Remove wet carpets, padding, and baseboards', description: 'Carpet padding acts like a sponge and rarely dries properly. Remove it promptly. Pull up baseboards to allow wall cavities to dry and prevent mold.', scenario: 'all' },
      { id: '3-6', title: 'Call professional water extraction service for extensive damage', description: 'For significant flooding (over 2 inches), professional equipment is necessary. They have industrial pumps, extractors, and drying equipment that work much faster.', scenario: 'flood' }
    ]
  },
  prevention: {
    title: 'Damage Prevention & Mitigation',
    icon: 'lucide-shield',
    color: 'text-green-500',
    items: [
      { id: '4-1', title: 'Cover roof leak with tarp or plastic sheeting', description: 'Secure a waterproof tarp over the leak from the outside if safe to do so. Extend it past the damaged area and weight down edges. This prevents additional water intrusion.', scenario: 'roof' },
      { id: '4-2', title: 'Inspect for additional leaks or weak spots', description: 'Water often travels through walls and ceilings before becoming visible. Check adjacent rooms, floors above and below, and inside cabinets for hidden water damage.', scenario: 'all' },
      { id: '4-3', title: 'Monitor for signs of mold growth (starts within 24-48 hours)', description: 'Mold can begin growing within 24-48 hours in damp conditions. Check for musty odors, visible spots, or discoloration. Act immediately if found.', scenario: 'all' },
      { id: '4-4', title: 'Place sandbags or barriers to redirect water flow', description: 'If flooding is ongoing or expected, sandbags can divert water away from entry points. Place them in doorways, garage openings, and low spots.', scenario: 'flood' },
      { id: '4-5', title: 'Seal off contaminated areas to prevent spread', description: 'Use plastic sheeting and tape to isolate sewage-affected areas. This prevents airborne contaminants from spreading to clean areas of your home.', scenario: 'sewage' }
    ]
  },
  professional: {
    title: 'Professional Services',
    icon: 'lucide-wrench',
    color: 'text-purple-500',
    items: [
      { id: '5-1', title: 'Contact a licensed plumber for pipe repairs', description: 'Burst pipes, leaking fixtures, and plumbing failures require professional repair. A licensed plumber can properly assess and fix the root cause.', scenario: 'burst-pipe' },
      { id: '5-2', title: 'Hire certified water damage restoration company', description: 'For significant damage, certified technicians have specialized equipment and training. Look for IICRC (Institute of Inspection, Cleaning and Restoration Certification) credentials.', scenario: 'all' },
      { id: '5-3', title: 'Schedule appliance inspection and repair', description: 'Have the leaking appliance inspected by a qualified technician. Determine if repair or replacement is necessary and address any warranty coverage.', scenario: 'appliance' },
      { id: '5-4', title: 'Arrange for mold inspection and remediation if needed', description: 'If mold is present or suspected, hire a certified mold remediation specialist. DIY mold cleanup is only appropriate for very small areas (less than 10 sq ft).', scenario: 'all' },
      { id: '5-5', title: 'Contact roofing contractor for repairs', description: 'Have a licensed roofer inspect and repair the damage. Get multiple estimates and ask about warranty coverage on repairs.', scenario: 'roof' },
      { id: '5-6', title: 'Hire specialized sewage cleanup professionals immediately', description: 'Sewage cleanup requires specialized equipment, protective gear, and proper disposal methods. Never attempt DIY sewage cleanup - it\'s a serious health hazard.', scenario: 'sewage' },
      { id: '5-7', title: 'Schedule electrical inspection before restoring power', description: 'Before turning electricity back on, have a licensed electrician inspect all affected circuits, outlets, and fixtures for safety.', scenario: 'all' }
    ]
  },
  recovery: {
    title: 'Recovery & Restoration',
    icon: 'lucide-home',
    color: 'text-amber-500',
    items: [
      { id: '6-1', title: 'Clean and disinfect all affected surfaces', description: 'Use appropriate cleaning solutions (diluted bleach for non-porous surfaces). This prevents bacterial growth and eliminates odors. Wear gloves and ensure ventilation.', scenario: 'all' },
      { id: '6-2', title: 'Replace damaged drywall, insulation, and flooring', description: 'Materials that stayed wet for more than 48 hours often need replacement. Drywall and insulation are difficult to fully dry and can harbor mold.', scenario: 'all' },
      { id: '6-3', title: 'Repaint walls and refinish surfaces', description: 'Once everything is thoroughly dry (use a moisture meter to verify), you can repaint. Consider mold-resistant paint in areas prone to moisture.', scenario: 'all' },
      { id: '6-4', title: 'Replace or professionally clean carpets and upholstery', description: 'Professional cleaning may save some items, but replacement is often necessary for heavily soaked materials or items exposed to contaminated water.', scenario: 'all' },
      { id: '6-5', title: 'Test for moisture levels before closing walls', description: 'Use a moisture meter to ensure materials are completely dry (typically below 15% moisture content) before sealing walls or installing new materials.', scenario: 'all' },
      { id: '6-6', title: 'Install moisture barriers or waterproofing in vulnerable areas', description: 'Prevent future issues by adding waterproofing, vapor barriers, or improved drainage in areas that experienced water damage.', scenario: 'all' },
      { id: '6-7', title: 'Review and implement prevention measures', description: 'Consider upgrades like a sump pump, water sensors, automatic shutoff valves, or regular appliance maintenance to prevent future water damage.', scenario: 'all' }
    ]
  }
}

// Computed properties
const overallProgress = computed(() => {
  let totalItems = 0
  let completedCount = 0

  Object.keys(checklistData).forEach(categoryKey => {
    const items = getFilteredItems(categoryKey, activeTab.value)
    totalItems += items.length
    completedCount += items.filter(item => completedItems.value.has(item.id)).length
  })

  return totalItems > 0 ? Math.round((completedCount / totalItems) * 100) : 0
})

// Methods
const getFilteredItems = (categoryKey: string, scenario: string) => {
  const category = checklistData[categoryKey]
  if (!category) return []
  
  let items = scenario === 'all' 
    ? category.items 
    : category.items.filter(item => item.scenario === scenario || item.scenario === 'all')
  
  // Apply search filter
  if (searchQuery.value) {
    const query = searchQuery.value.toLowerCase()
    items = items.filter(item => 
      item.title.toLowerCase().includes(query) || 
      item.description.toLowerCase().includes(query)
    )
  }
  
  return items
}

const getCategoryProgress = (categoryKey: string, scenario: string) => {
  const items = getFilteredItems(categoryKey, scenario)
  if (items.length === 0) return 0
  
  const completed = items.filter(item => completedItems.value.has(item.id)).length
  return Math.round((completed / items.length) * 100)
}

const getScenarioProgress = (scenario: string) => {
  let totalItems = 0
  let completedCount = 0
  
  Object.keys(checklistData).forEach(categoryKey => {
    const items = getFilteredItems(categoryKey, scenario)
    totalItems += items.length
    completedCount += items.filter(item => completedItems.value.has(item.id)).length
  })
  
  return totalItems > 0 ? Math.round((completedCount / totalItems) * 100) : 0
}

const getScenarioStyle = (scenario: string) => {
  const styles: Record<string, string> = {
    'all': 'bg-gray-100 text-gray-700 border-gray-300',
    'burst-pipe': 'bg-blue-100 text-blue-700 border-blue-300',
    'flood': 'bg-cyan-100 text-cyan-700 border-cyan-300',
    'appliance': 'bg-purple-100 text-purple-700 border-purple-300',
    'roof': 'bg-green-100 text-green-700 border-green-300',
    'sewage': 'bg-red-100 text-red-700 border-red-300'
  }
  return styles[scenario] || styles['all']
}

const toggleItem = (itemId: string) => {
  if (completedItems.value.has(itemId)) {
    completedItems.value.delete(itemId)
  } else {
    completedItems.value.add(itemId)
  }
  saveProgress()
}

const toggleExpertTip = (itemId: string) => {
  if (visibleExpertTips.value.has(itemId)) {
    visibleExpertTips.value.delete(itemId)
  } else {
    visibleExpertTips.value.add(itemId)
  }
}

const resetProgress = () => {
  if (confirm('Are you sure you want to reset all progress? This cannot be undone.')) {
    completedItems.value.clear()
    saveProgress()
  }
}

const saveProgress = () => {
  if (typeof window !== 'undefined') {
    localStorage.setItem('waterDamageChecklistProgress', JSON.stringify(Array.from(completedItems.value)))
  }
}

const loadProgress = () => {
  if (typeof window !== 'undefined') {
    const saved = localStorage.getItem('waterDamageChecklistProgress')
    if (saved) {
      completedItems.value = new Set(JSON.parse(saved))
    }
  }
}

const downloadPDF = () => {
  // Placeholder for PDF generation
  alert('PDF download functionality would be implemented here. This would generate a printable checklist with your current progress.')
}

// Lifecycle
onMounted(() => {
  loadProgress()
})
</script>

<style scoped>
@keyframes fade-in-up {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-fade-in-up {
  animation: fade-in-up 0.6s ease-out;
}

.animation-delay-200 {
  animation-delay: 0.2s;
  animation-fill-mode: both;
}

.animation-delay-400 {
  animation-delay: 0.4s;
  animation-fill-mode: both;
}

.animation-delay-700 {
  animation-delay: 0.7s;
  animation-fill-mode: both;
}

.animation-delay-800 {
  animation-delay: 0.8s;
  animation-fill-mode: both;
}

.animation-delay-1000 {
  animation-delay: 1s;
  animation-fill-mode: both;
}
</style>

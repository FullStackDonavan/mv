<!-- components/WaterDamageEstimator.vue -->
<template>
  <section class="py-16 bg-gray-50">
    <div class="container mx-auto px-4 max-w-6xl">
      <!-- Header -->
      <div class="text-center mb-12">
        <div class="inline-flex items-center rounded-full border px-2.5 py-0.5 text-xs font-semibold transition-colors focus:outline-none focus:ring-2 focus:ring-ring focus:ring-offset-2 mb-4 text-gray-900 border-[#FFEE50]/50 bg-[#FFEE50]/90">
          Property Damage Assessment
        </div>
        <h1 class="text-3xl font-bold mb-4 text-gray-800">
          Water Damage Estimator
        </h1>
        <p class="text-gray-600 max-w-3xl mx-auto">
          Get an instant estimate of water damage restoration costs based on the affected area and severity.
        </p>
      </div>

      <div class="lg:flex lg:gap-8">
        <!-- Calculator Form -->
        <div class="bg-white rounded-2xl shadow-2xl overflow-hidden transition-all duration-700 ease-out" :class="result ? 'lg:w-1/2' : 'lg:w-full'">
          <!-- Form Header -->
          <div class="bg-gradient-to-r from-[#FFEE50] to-[#FFD700] py-6 px-8">
            <h3 class="text-xl font-semibold text-gray-900 text-center">
              Enter Damage Details
            </h3>
            <p class="text-gray-700 text-center text-sm mt-1">Provide information about the water damage for an estimate</p>
          </div>

          <div class="p-8 flex flex-col transition-all duration-700 ease-out" :class="result ? 'h-[750px]' : 'min-h-[400px]'">
            <div class="flex-1 overflow-auto">
              <form @submit.prevent="calculate" class="space-y-6">
              <!-- Affected Area & Water Category -->
              <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div class="space-y-3">
                  <label for="affectedArea" class="text-sm font-semibold text-gray-700">Affected Area (sq ft)</label>
                  <input 
                    type="number" 
                    id="affectedArea" 
                    v-model.number="affectedArea" 
                    class="w-full h-14 px-4 rounded-xl border-2 border-gray-200 bg-white text-gray-800 focus:outline-none focus:border-[#FFEE50] focus:ring-4 focus:ring-[#FFEE50]/20 transition-all duration-300 text-lg" 
                    min="0"
                    placeholder="e.g., 500"
                  />
                </div>
                <div class="space-y-3">
                  <label for="waterCategory" class="text-sm font-semibold text-gray-700">Water Category</label>
                  <select 
                    id="waterCategory" 
                    v-model="waterCategory" 
                    class="w-full h-14 px-4 rounded-xl border-2 border-gray-200 bg-white text-gray-800 focus:outline-none focus:border-[#FFEE50] focus:ring-4 focus:ring-[#FFEE50]/20 transition-all duration-300 text-lg"
                  >
                    <option value="clean">Clean Water (Cat 1)</option>
                    <option value="gray">Gray Water (Cat 2)</option>
                    <option value="black">Black Water (Cat 3)</option>
                  </select>
                </div>
              </div>

              <!-- Room Type & Damage Class -->
              <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div class="space-y-3">
                  <label for="roomType" class="text-sm font-semibold text-gray-700">Room Type</label>
                  <select 
                    id="roomType" 
                    v-model="roomType" 
                    class="w-full h-14 px-4 rounded-xl border-2 border-gray-200 bg-white text-gray-800 focus:outline-none focus:border-[#FFEE50] focus:ring-4 focus:ring-[#FFEE50]/20 transition-all duration-300 text-lg"
                  >
                    <option value="bathroom">Bathroom</option>
                    <option value="kitchen">Kitchen</option>
                    <option value="bedroom">Bedroom</option>
                    <option value="living">Living Room</option>
                    <option value="basement">Basement</option>
                    <option value="other">Other</option>
                  </select>
                </div>
                <div class="space-y-3">
                  <label for="damageClass" class="text-sm font-semibold text-gray-700">Damage Class</label>
                  <select 
                    id="damageClass" 
                    v-model="damageClass" 
                    class="w-full h-14 px-4 rounded-xl border-2 border-gray-200 bg-white text-gray-800 focus:outline-none focus:border-[#FFEE50] focus:ring-4 focus:ring-[#FFEE50]/20 transition-all duration-300 text-lg"
                  >
                    <option value="1">Class 1 - Minimal</option>
                    <option value="2">Class 2 - Significant</option>
                    <option value="3">Class 3 - Extensive</option>
                    <option value="4">Class 4 - Specialty</option>
                  </select>
                </div>
              </div>

              <!-- Additional Factors -->
              <div class="space-y-3">
                <label class="text-sm font-semibold text-gray-700 block mb-2">Additional Services Needed</label>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                  <label class="flex items-center space-x-3 cursor-pointer">
                    <input 
                      type="checkbox" 
                      v-model="moldRemediation" 
                      class="w-5 h-5 rounded border-gray-300 text-[#FFEE50] focus:ring-[#FFEE50]"
                    />
                    <span class="text-gray-700">Mold Remediation</span>
                  </label>
                  <label class="flex items-center space-x-3 cursor-pointer">
                    <input 
                      type="checkbox" 
                      v-model="carpetReplacement" 
                      class="w-5 h-5 rounded border-gray-300 text-[#FFEE50] focus:ring-[#FFEE50]"
                    />
                    <span class="text-gray-700">Carpet Replacement</span>
                  </label>
                  <label class="flex items-center space-x-3 cursor-pointer">
                    <input 
                      type="checkbox" 
                      v-model="drywallReplacement" 
                      class="w-5 h-5 rounded border-gray-300 text-[#FFEE50] focus:ring-[#FFEE50]"
                    />
                    <span class="text-gray-700">Drywall Replacement</span>
                  </label>
                  <label class="flex items-center space-x-3 cursor-pointer">
                    <input 
                      type="checkbox" 
                      v-model="emergencyService" 
                      class="w-5 h-5 rounded border-gray-300 text-[#FFEE50] focus:ring-[#FFEE50]"
                    />
                    <span class="text-gray-700">Emergency Service</span>
                  </label>
                </div>
              </div>
              </form>
            </div>

            <!-- Submit Button Section - Always at bottom -->
            <div class="pt-4">
              <button 
                type="submit" 
                @click="calculate" 
                  class="w-full bg-gradient-to-r from-[#FFEE50] to-[#FFD700] text-gray-900 px-8 py-4 rounded-xl hover:from-[#FFD700] hover:to-[#FFC700] transition-all duration-300 transform hover:scale-105 font-semibold text-lg shadow-lg"
                >
                  <span class="flex items-center justify-center gap-2">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 7h6m0 10v-3m-3 3h.01M9 17h.01M9 14h.01M12 14h.01M15 11h.01M12 11h.01M9 11h.01M7 21h10a2 2 0 002-2V5a2 2 0 00-2-2H7a2 2 0 00-2 2v14a2 2 0 002 2z"/>
                    </svg>
                    Calculate Estimate
                  </span>
                </button>
              </div>
          </div>
        </div>

        <!-- Results Panel -->
        <div v-if="result" class="lg:w-1/2 mt-8 lg:mt-0">
          <div class="bg-white rounded-2xl shadow-2xl overflow-hidden">
                <!-- Results Header -->
                <div class="bg-gradient-to-r from-green-500 to-emerald-600 py-6 px-8">
                  <h3 class="text-xl font-semibold text-white text-center">
                    Your Water Damage Estimate
                  </h3>
                  <p class="text-white/80 text-center text-sm mt-1">Estimated Restoration Costs</p>
                </div>

              <div class="p-8 bg-gradient-to-br from-gray-50 to-white">
                <!-- Key Metrics -->
                <div class="grid grid-cols-1 gap-6 mb-6">
                  <div class="bg-gradient-to-br from-[#FFEE50]/30 to-[#FFD700]/10 rounded-xl border-2 border-[#FFEE50]/50 p-6 text-center shadow-lg">
                    <div class="text-gray-600 mb-2 font-medium">Estimated Total Cost</div>
                    <p class="text-4xl font-bold text-gray-900">${{ formattedTotal }}</p>
                    <div class="mt-4 pt-4 border-t border-gray-200">
                      <div class="grid grid-cols-2 gap-4 text-sm">
                        <div>
                          <p class="text-gray-500">Low Estimate</p>
                          <p class="font-semibold text-gray-700">${{ formattedLow }}</p>
                        </div>
                        <div>
                          <p class="text-gray-500">High Estimate</p>
                          <p class="font-semibold text-gray-700">${{ formattedHigh }}</p>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Cost Breakdown -->
                <div class="bg-white rounded-xl border-2 border-gray-200 p-6 mb-6">
                  <h4 class="font-semibold text-gray-800 mb-4 text-lg">Cost Breakdown</h4>
                  <div class="space-y-3">
                    <div class="flex justify-between items-center pb-2 border-b border-gray-100">
                      <span class="text-gray-600">Water Extraction & Drying</span>
                      <span class="font-semibold text-gray-800">${{ formattedExtraction }}</span>
                    </div>
                    <div class="flex justify-between items-center pb-2 border-b border-gray-100">
                      <span class="text-gray-600">Base Restoration</span>
                      <span class="font-semibold text-gray-800">${{ formattedRestoration }}</span>
                    </div>
                    <div v-if="additionalCosts > 0" class="flex justify-between items-center pb-2 border-b border-gray-100">
                      <span class="text-gray-600">Additional Services</span>
                      <span class="font-semibold text-gray-800">${{ formattedAdditional }}</span>
                    </div>
                  </div>
                </div>

                <!-- Timeline Estimate -->
                <div class="bg-gradient-to-br from-blue-50 to-indigo-50 border-2 border-blue-200 p-6 rounded-xl mb-6">
                  <div class="flex items-start gap-3">
                    <svg class="w-8 h-8 text-blue-600 flex-shrink-0 mt-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                    </svg>
                    <div>
                      <h4 class="font-semibold text-blue-900 mb-2">Estimated Timeline</h4>
                      <p class="text-blue-800">{{ estimatedTimeline }}</p>
                    </div>
                  </div>
                </div>

                <!-- Important Notice -->
                <div class="bg-yellow-50 border-2 border-yellow-200 p-6 rounded-xl">
                  <div class="flex items-start gap-3">
                    <svg class="w-6 h-6 text-yellow-600 flex-shrink-0 mt-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                    </svg>
                    <div>
                      <h4 class="font-semibold text-yellow-900 mb-2">Important Note</h4>
                      <p class="text-yellow-800 text-sm">This is an estimate only. Actual costs may vary based on specific conditions, local labor rates, and unforeseen complications. Contact a professional for an accurate assessment.</p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'

const affectedArea = ref(500)
const waterCategory = ref('clean')
const roomType = ref('bathroom')
const damageClass = ref('2')
const moldRemediation = ref(false)
const carpetReplacement = ref(false)
const drywallReplacement = ref(false)
const emergencyService = ref(false)

const result = ref(false)
const totalCost = ref(0)
const lowEstimate = ref(0)
const highEstimate = ref(0)
const extractionCost = ref(0)
const restorationCost = ref(0)
const additionalCosts = ref(0)
const estimatedTimeline = ref('')

const calculate = () => {
  // Base cost per square foot based on water category
  const categoryMultipliers = {
    clean: 3.75,  // $3-4.50/sq ft
    gray: 4.50,   // $4-5/sq ft
    black: 7.00   // $7-7.50/sq ft
  }

  // Damage class multiplier
  const classMultipliers = {
    '1': 1.0,
    '2': 1.25,
    '3': 1.5,
    '4': 2.0
  }

  // Room type adjustment
  const roomMultipliers = {
    bathroom: 1.2,
    kitchen: 1.3,
    bedroom: 1.0,
    living: 1.1,
    basement: 0.9,
    other: 1.0
  }

  // Calculate base extraction and drying cost
  const baseRate = categoryMultipliers[waterCategory.value]
  extractionCost.value = affectedArea.value * baseRate

  // Calculate restoration cost
  const classMultiplier = classMultipliers[damageClass.value]
  const roomMultiplier = roomMultipliers[roomType.value]
  restorationCost.value = extractionCost.value * classMultiplier * roomMultiplier

  // Calculate additional costs
  let additionalTotal = 0
  if (moldRemediation.value) {
    additionalTotal += affectedArea.value * 2.5 // $2-3/sq ft
  }
  if (carpetReplacement.value) {
    additionalTotal += affectedArea.value * 4 // $3-5/sq ft
  }
  if (drywallReplacement.value) {
    additionalTotal += affectedArea.value * 2 // $1.50-2.50/sq ft
  }
  if (emergencyService.value) {
    additionalTotal += 500 // Flat emergency fee
  }
  additionalCosts.value = additionalTotal

  // Calculate total with range
  const baseCost = extractionCost.value + restorationCost.value + additionalCosts.value
  totalCost.value = baseCost
  lowEstimate.value = baseCost * 0.85
  highEstimate.value = baseCost * 1.15

  // Estimate timeline
  const days = Math.ceil(affectedArea.value / 200) + parseInt(damageClass.value)
  if (days <= 3) {
    estimatedTimeline.value = `${days} days - Quick turnaround for minimal damage`
  } else if (days <= 7) {
    estimatedTimeline.value = `${days} days - Standard restoration timeline`
  } else {
    estimatedTimeline.value = `${days} days - Extended restoration for severe damage`
  }

  result.value = true
}

const formattedTotal = computed(() =>
  totalCost.value.toLocaleString(undefined, { maximumFractionDigits: 0 })
)
const formattedLow = computed(() =>
  lowEstimate.value.toLocaleString(undefined, { maximumFractionDigits: 0 })
)
const formattedHigh = computed(() =>
  highEstimate.value.toLocaleString(undefined, { maximumFractionDigits: 0 })
)
const formattedExtraction = computed(() =>
  extractionCost.value.toLocaleString(undefined, { maximumFractionDigits: 0 })
)
const formattedRestoration = computed(() =>
  restorationCost.value.toLocaleString(undefined, { maximumFractionDigits: 0 })
)
const formattedAdditional = computed(() =>
  additionalCosts.value.toLocaleString(undefined, { maximumFractionDigits: 0 })
)
</script>

<style scoped>
/* Card hover effects matching the form styling */
.bg-white.rounded-2xl {
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

/* Enhanced input focus effects */
input:focus, select:focus {
  transform: translateY(-2px) scale(1.01);
  box-shadow: 0 12px 30px rgba(255, 238, 80, 0.4);
}

/* Enhanced button hover effects */
button {
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

button:hover:not(:disabled) {
  transform: translateY(-2px) scale(1.02);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

button:active:not(:disabled) {
  transform: translateY(0) scale(0.98);
}

/* Stagger animation for form fields */
.space-y-6 > div:nth-child(1) {
  animation: slideInUp 0.6s cubic-bezier(0.4, 0, 0.2, 1) 0.1s both;
}

.space-y-6 > div:nth-child(2) {
  animation: slideInUp 0.6s cubic-bezier(0.4, 0, 0.2, 1) 0.2s both;
}

.space-y-6 > div:nth-child(3) {
  animation: slideInUp 0.6s cubic-bezier(0.4, 0, 0.2, 1) 0.3s both;
}

@keyframes slideInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Badge styling */
.inline-flex {
  transition: all 0.3s ease-in-out;
}

.inline-flex:hover {
  transform: scale(1.05);
  background-color: rgba(255, 238, 80, 0.95);
}

/* Icon animations */
svg {
  transition: all 0.3s ease-in-out;
}

/* Checkbox styling */
input[type="checkbox"] {
  cursor: pointer;
  transition: all 0.2s ease-in-out;
}

input[type="checkbox"]:checked {
  background-color: #FFEE50;
  border-color: #FFEE50;
}

/* Mobile responsiveness */
@media (max-width: 768px) {
  input:focus, select:focus {
    transform: translateY(-1px) scale(1.005);
  }
}

/* Enhanced focus states for accessibility */
.bg-white.rounded-2xl:focus-within {
  outline: 2px solid #FFEE50;
  outline-offset: 2px;
}
</style>

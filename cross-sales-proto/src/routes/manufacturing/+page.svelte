<script>
  import { onMount } from 'svelte';
  import Building from '$lib/icons/Building.svelte';
  import Users from '$lib/icons/Users.svelte';
  import Shield from '$lib/icons/Shield.svelte';
  import AlertTriangle from '$lib/icons/AlertTriangle.svelte';
  import Check from '$lib/icons/Check.svelte';
  import ArrowLeft from '$lib/icons/ArrowLeft.svelte';
  import ArrowRight from '$lib/icons/ArrowRight.svelte';
  import Mail from '$lib/icons/Mail.svelte';
  import Phone from '$lib/icons/Phone.svelte';
  import Globe from '$lib/icons/Globe.svelte';
  
  let currentStep = $state(1);
  let companyData = {
    name: "Nordic Manufacturing AB",
    employees: 25,
    industry: "Manufacturing",
    currentPolicies: ["General Liability"],
    riskFactors: ["Growing workforce", "Product liability exposure", "International expansion"]
  };
  
  let journeySteps = [
    {
      day: 1,
      title: "Portal Activity",
      channel: "MyBusiness Portal",
      action: "Employee count update (25 → 40)",
      recommendation: "Workers' Compensation + Product Liability",
      status: "viewed"
    },
    {
      day: 3,
      title: "Email Follow-up",
      channel: "Email",
      action: "Targeted campaign",
      recommendation: "Protection for growing workforce",
      status: "clicked"
    },
    {
      day: 5,
      title: "Webshop Engagement",
      channel: "Digital Webshop",
      action: "Quote generation",
      recommendation: "Workers' Comp (€4,200) + Product Liability (€3,100)",
      status: "saved"
    },
    {
      day: 7,
      title: "Account Manager Call",
      channel: "Phone",
      action: "Personalized consultation",
      recommendation: "Bundle discount + Group Life",
      status: "converted"
    }
  ];

  function nextStep() {
    if (currentStep < journeySteps.length) {
      currentStep++;
    }
  }

  function prevStep() {
    if (currentStep > 1) {
      currentStep--;
    }
  }

  function getChannelIcon(channel) {
    switch(channel) {
      case 'MyBusiness Portal': return Globe;
      case 'Email': return Mail;
      case 'Digital Webshop': return Globe;
      case 'Phone': return Phone;
      default: return Globe;
    }
  }

  function getStatusColor(status) {
    switch(status) {
      case 'viewed': return 'bg-blue-100 text-blue-800';
      case 'clicked': return 'bg-yellow-100 text-yellow-800';
      case 'saved': return 'bg-orange-100 text-orange-800';
      case 'converted': return 'bg-green-100 text-green-800';
      default: return 'bg-gray-100 text-gray-800';
    }
  }
</script>

<div class="container mx-auto px-6 py-8">
  <!-- Header -->
  <div class="mb-8">
    <a href="/" class="inline-flex items-center text-primary-600 hover:text-primary-700 mb-4">
      <ArrowLeft class="h-4 w-4 mr-2" />
      Back to Scenarios
    </a>
    
    <div class="bg-white rounded-lg shadow-md p-6">
      <div class="flex items-center mb-4">
        <Building class="h-8 w-8 text-primary-600 mr-3" />
        <div>
          <h1 class="text-2xl font-bold text-nordic-900">{companyData.name}</h1>
          <p class="text-nordic-600">Manufacturing Company Cross-Sales Journey</p>
        </div>
      </div>
      
      <div class="grid md:grid-cols-4 gap-4">
        <div class="flex items-center">
          <Users class="h-5 w-5 text-nordic-500 mr-2" />
          <span class="text-sm"><strong>{companyData.employees}</strong> employees</span>
        </div>
        <div class="flex items-center">
          <Shield class="h-5 w-5 text-nordic-500 mr-2" />
          <span class="text-sm"><strong>{companyData.currentPolicies.length}</strong> current policy</span>
        </div>
        <div class="flex items-center">
          <AlertTriangle class="h-5 w-5 text-orange-500 mr-2" />
          <span class="text-sm"><strong>High</strong> growth phase</span>
        </div>
        <div class="flex items-center">
          <Check class="h-5 w-5 text-green-500 mr-2" />
          <span class="text-sm"><strong>Digital</strong> preferred</span>
        </div>
      </div>
    </div>
  </div>

  <!-- Journey Timeline -->
  <div class="bg-white rounded-lg shadow-md p-6 mb-8">
    <h2 class="text-xl font-semibold text-nordic-800 mb-6">Omni-Channel Cross-Sales Journey</h2>
    
    <!-- Progress Bar -->
    <div class="mb-8">
      <div class="flex justify-between mb-2">
        {#each journeySteps as step, index}
          <div class="flex flex-col items-center">
            <div class="w-8 h-8 rounded-full flex items-center justify-center text-sm font-medium
                        {index + 1 <= currentStep ? 'bg-primary-600 text-white' : 'bg-nordic-200 text-nordic-600'}">
              {step.day}
            </div>
            <span class="text-xs text-nordic-600 mt-1">Day {step.day}</span>
          </div>
        {/each}
      </div>
      <div class="w-full bg-nordic-200 rounded-full h-2">
        <div class="bg-primary-600 h-2 rounded-full transition-all duration-500 ease-in-out" 
             style="width: {(currentStep / journeySteps.length) * 100}%"></div>
      </div>
    </div>

    <!-- Current Step Detail -->
    {#if journeySteps[currentStep - 1]}
      {@const step = journeySteps[currentStep - 1]}
      {@const ChannelIcon = getChannelIcon(step.channel)}
      
      <div class="border-2 border-primary-200 rounded-lg p-6">
        <div class="flex items-center justify-between mb-4">
          <div class="flex items-center">
            <ChannelIcon class="h-6 w-6 text-primary-600 mr-3" />
            <div>
              <h3 class="text-lg font-semibold text-nordic-800">{step.title}</h3>
              <p class="text-nordic-600">{step.channel}</p>
            </div>
          </div>
          <span class="px-3 py-1 rounded-full text-sm font-medium {getStatusColor(step.status)}">
            {step.status.charAt(0).toUpperCase() + step.status.slice(1)}
          </span>
        </div>
        
        <div class="grid md:grid-cols-2 gap-6">
          <div>
            <h4 class="font-medium text-nordic-800 mb-2">Customer Action</h4>
            <p class="text-nordic-600">{step.action}</p>
          </div>
          <div>
            <h4 class="font-medium text-nordic-800 mb-2">System Recommendation</h4>
            <p class="text-nordic-600">{step.recommendation}</p>
          </div>
        </div>

        <!-- Step-specific content -->
        {#if currentStep === 1}
          <div class="mt-6 p-4 bg-nordic-50 rounded-lg">
            <div class="notification">
              <div class="flex items-center">
                <AlertTriangle class="h-5 w-5 text-primary-600 mr-2" />
                <span class="font-medium">Growth Detected:</span>
              </div>
              <p class="mt-2">Your expansion from 25 to 40 employees may require enhanced protection. Consider Workers' Compensation and Product Liability coverage.</p>
              <button class="btn-primary mt-3">Review Recommendations</button>
            </div>
          </div>
        {:else if currentStep === 2}
          <div class="mt-6 p-4 bg-nordic-50 rounded-lg">
            <div class="bg-white border border-nordic-200 rounded-lg p-4">
              <div class="flex items-center mb-2">
                <Mail class="h-5 w-5 text-primary-600 mr-2" />
                <strong>Email: Protect Your Growing Workforce</strong>
              </div>
              <p class="text-sm text-nordic-600 mb-3">Based on your recent employee count update, we've identified coverage gaps that could impact your business.</p>
              <ul class="text-sm text-nordic-600 space-y-1">
                <li>• Workers' Compensation: Protect your expanded team</li>
                <li>• Product Liability: Safeguard against manufacturing risks</li>
              </ul>
              <button class="btn-secondary mt-3 text-sm">Get Instant Quote</button>
            </div>
          </div>
        {:else if currentStep === 3}
          <div class="mt-6 p-4 bg-nordic-50 rounded-lg">
            <div class="grid md:grid-cols-2 gap-4">
              <div class="bg-white border border-nordic-200 rounded-lg p-4">
                <h5 class="font-medium text-nordic-800 mb-2">Workers' Compensation</h5>
                <p class="text-2xl font-bold text-primary-600">€4,200</p>
                <p class="text-sm text-nordic-600">Annual premium for 40 employees</p>
                <button class="btn-secondary w-full mt-3">Add to Quote</button>
              </div>
              <div class="bg-white border border-nordic-200 rounded-lg p-4">
                <h5 class="font-medium text-nordic-800 mb-2">Product Liability</h5>
                <p class="text-2xl font-bold text-primary-600">€3,100</p>
                <p class="text-sm text-nordic-600">€5M coverage limit</p>
                <button class="btn-secondary w-full mt-3">Add to Quote</button>
              </div>
            </div>
          </div>
        {:else if currentStep === 4}
          <div class="mt-6 p-4 bg-nordic-50 rounded-lg">
            <div class="bg-green-50 border border-green-200 rounded-lg p-4">
              <div class="flex items-center mb-3">
                <Check class="h-6 w-6 text-green-600 mr-2" />
                <span class="font-semibold text-green-800">Conversion Successful!</span>
              </div>
              <div class="grid md:grid-cols-3 gap-4 text-sm">
                <div>
                  <strong>Workers' Compensation:</strong>
                  <p class="text-green-700">€4,200/year</p>
                </div>
                <div>
                  <strong>Product Liability:</strong>
                  <p class="text-green-700">€3,100/year</p>
                </div>
                <div>
                  <strong>Group Life (Bonus):</strong>
                  <p class="text-green-700">€1,800/year</p>
                </div>
              </div>
              <p class="mt-3 font-medium text-green-800">Total Additional Premium: €9,100/year</p>
            </div>
          </div>
        {/if}
      </div>

      <!-- Navigation -->
      <div class="flex justify-between mt-6">
        <button 
          onclick={prevStep} 
          disabled={currentStep === 1}
          class="btn-secondary disabled:opacity-50 disabled:cursor-not-allowed">
          <ArrowLeft class="h-4 w-4 mr-2" />
          Previous
        </button>
        
        <button 
          onclick={nextStep} 
          disabled={currentStep === journeySteps.length}
          class="btn-primary disabled:opacity-50 disabled:cursor-not-allowed">
          Next
          <ArrowRight class="h-4 w-4 ml-2" />
        </button>
      </div>
    {/if}
  </div>

  <!-- Key Insights -->
  <div class="bg-white rounded-lg shadow-md p-6">
    <h2 class="text-xl font-semibold text-nordic-800 mb-4">Omni-Channel Benefits Demonstrated</h2>
    
    <div class="grid md:grid-cols-2 gap-6">
      <div>
        <h4 class="font-medium text-nordic-800 mb-2">Cross-Channel Consistency</h4>
        <ul class="text-nordic-600 text-sm space-y-1">
          <li>• Employee count automatically synced across all channels</li>
          <li>• Consistent pricing and recommendations</li>
          <li>• No need for customers to repeat information</li>
        </ul>
      </div>
      
      <div>
        <h4 class="font-medium text-nordic-800 mb-2">Progressive Engagement</h4>
        <ul class="text-nordic-600 text-sm space-y-1">
          <li>• Self-service portal for initial discovery</li>
          <li>• Targeted email for deeper engagement</li>
          <li>• Human expertise for final conversion</li>
        </ul>
      </div>
    </div>
  </div>
</div>
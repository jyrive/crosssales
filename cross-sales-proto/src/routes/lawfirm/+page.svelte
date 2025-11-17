<script>
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
    name: "Bergström & Partners Law Firm",
    employees: 8,
    partners: 8,
    industry: "Legal Services",
    currentPolicies: ["Professional Indemnity"],
    customerType: "Traditional",
    preferences: ["Human interaction", "Phone calls", "Personal meetings", "Physical mail"]
  };
  
  let journeySteps = [
    {
      week: 1,
      title: "Annual Review Trigger",
      channel: "Internal System",
      action: "PI renewal reminder + D&O gap identification",
      recommendation: "Directors & Officers coverage for partners",
      status: "identified"
    },
    {
      week: 2,
      title: "Relationship Manager Preparation",
      channel: "CRM",
      action: "Account manager receives D&O opportunity alert",
      recommendation: "Prepare personalized D&O proposal",
      status: "prepared"
    },
    {
      week: 4,
      title: "Routine Check-in Call",
      channel: "Phone",
      action: "PI renewal discussion + gentle D&O introduction",
      recommendation: "D&O coverage for partnership protection",
      status: "interested"
    },
    {
      week: 6,
      title: "Information Package",
      channel: "Physical Mail",
      action: "Detailed D&O brochure with personalized letter",
      recommendation: "€8,000 D&O coverage with partnership focus",
      status: "reviewing"
    },
    {
      week: 8,
      title: "Follow-up Discussion",
      channel: "Phone",
      action: "Partner meeting to discuss D&O benefits",
      recommendation: "Customized D&O proposal with legal sector focus",
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
      case 'Internal System': return Globe;
      case 'CRM': return Globe;
      case 'Phone': return Phone;
      case 'Physical Mail': return Mail;
      default: return Globe;
    }
  }

  function getStatusColor(status) {
    switch(status) {
      case 'identified': return 'bg-blue-100 text-blue-800';
      case 'prepared': return 'bg-purple-100 text-purple-800';
      case 'interested': return 'bg-yellow-100 text-yellow-800';
      case 'reviewing': return 'bg-orange-100 text-orange-800';
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
        <Shield class="h-8 w-8 text-primary-600 mr-3" />
        <div>
          <h1 class="text-2xl font-bold text-nordic-900">{companyData.name}</h1>
          <p class="text-nordic-600">Traditional Law Firm - Human-Centric Cross-Sales</p>
        </div>
      </div>
      
      <div class="grid md:grid-cols-4 gap-4">
        <div class="flex items-center">
          <Users class="h-5 w-5 text-nordic-500 mr-2" />
          <span class="text-sm"><strong>{companyData.partners}</strong> partners</span>
        </div>
        <div class="flex items-center">
          <Shield class="h-5 w-5 text-nordic-500 mr-2" />
          <span class="text-sm"><strong>{companyData.currentPolicies.length}</strong> current policy</span>
        </div>
        <div class="flex items-center">
          <Phone class="h-5 w-5 text-blue-500 mr-2" />
          <span class="text-sm"><strong>Traditional</strong> approach</span>
        </div>
        <div class="flex items-center">
          <Check class="h-5 w-5 text-green-500 mr-2" />
          <span class="text-sm"><strong>Relationship</strong> focused</span>
        </div>
      </div>
    </div>
  </div>

  <!-- Journey Timeline -->
  <div class="bg-white rounded-lg shadow-md p-6 mb-8">
    <h2 class="text-xl font-semibold text-nordic-800 mb-6">Human-Centric Cross-Sales Journey</h2>
    
    <!-- Progress Bar -->
    <div class="mb-8">
      <div class="flex justify-between mb-2">
        {#each journeySteps as step, index}
          <div class="flex flex-col items-center">
            <div class="w-8 h-8 rounded-full flex items-center justify-center text-sm font-medium
                        {index + 1 <= currentStep ? 'bg-primary-600 text-white' : 'bg-nordic-200 text-nordic-600'}">
              {step.week}
            </div>
            <span class="text-xs text-nordic-600 mt-1">Week {step.week}</span>
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
            <h4 class="font-medium text-nordic-800 mb-2">Process Action</h4>
            <p class="text-nordic-600">{step.action}</p>
          </div>
          <div>
            <h4 class="font-medium text-nordic-800 mb-2">Recommendation</h4>
            <p class="text-nordic-600">{step.recommendation}</p>
          </div>
        </div>

        <!-- Step-specific content -->
        {#if currentStep === 1}
          <div class="mt-6 p-4 bg-nordic-50 rounded-lg">
            <div class="bg-blue-50 border border-blue-200 rounded-lg p-4">
              <div class="flex items-center mb-2">
                <AlertTriangle class="h-5 w-5 text-blue-600 mr-2" />
                <strong>System Alert: Coverage Gap Detected</strong>
              </div>
              <p class="text-sm text-blue-700 mb-3">Partnership structure with 8 partners lacks D&O protection. Partners personally exposed to management liability claims.</p>
              <div class="bg-white border border-blue-200 rounded p-3">
                <p class="text-sm font-medium text-blue-800">Recommended Action:</p>
                <p class="text-sm text-blue-700">Schedule D&O discussion during PI renewal conversation with relationship manager.</p>
              </div>
            </div>
          </div>
        {:else if currentStep === 2}
          <div class="mt-6 p-4 bg-nordic-50 rounded-lg">
            <div class="bg-purple-50 border border-purple-200 rounded-lg p-4">
              <div class="flex items-center mb-3">
                <Users class="h-5 w-5 text-purple-600 mr-2" />
                <strong>Account Manager Dashboard</strong>
              </div>
              <div class="grid md:grid-cols-2 gap-4 text-sm">
                <div>
                  <p class="font-medium text-purple-800 mb-1">Client Profile:</p>
                  <ul class="text-purple-700 space-y-1">
                    <li>• 15-year client relationship</li>
                    <li>• Traditional communication preference</li>
                    <li>• High trust in personal advice</li>
                  </ul>
                </div>
                <div>
                  <p class="font-medium text-purple-800 mb-1">Opportunity:</p>
                  <ul class="text-purple-700 space-y-1">
                    <li>• D&O coverage gap: €8,000 premium</li>
                    <li>• Legal sector specific risks</li>
                    <li>• Partnership liability exposure</li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        {:else if currentStep === 3}
          <div class="mt-6 p-4 bg-nordic-50 rounded-lg">
            <div class="bg-yellow-50 border border-yellow-200 rounded-lg p-4">
              <div class="flex items-center mb-3">
                <Phone class="h-5 w-5 text-yellow-600 mr-2" />
                <strong>Relationship Manager Call</strong>
              </div>
              <div class="space-y-3 text-sm">
                <div class="bg-white border border-yellow-200 rounded p-3">
                  <p class="font-medium text-yellow-800">"How's the firm doing, Lars?"</p>
                  <p class="text-yellow-700 mt-1">Natural conversation about business growth and challenges</p>
                </div>
                <div class="bg-white border border-yellow-200 rounded p-3">
                  <p class="font-medium text-yellow-800">"We're seeing more management liability cases in the legal sector..."</p>
                  <p class="text-yellow-700 mt-1">Gentle introduction of D&O risks without pressure</p>
                </div>
                <div class="bg-white border border-yellow-200 rounded p-3">
                  <p class="font-medium text-yellow-800">"Would you like me to send some information about D&O coverage?"</p>
                  <p class="text-yellow-700 mt-1">Partner expresses interest in learning more</p>
                </div>
              </div>
            </div>
          </div>
        {:else if currentStep === 4}
          <div class="mt-6 p-4 bg-nordic-50 rounded-lg">
            <div class="bg-orange-50 border border-orange-200 rounded-lg p-4">
              <div class="flex items-center mb-3">
                <Mail class="h-5 w-5 text-orange-600 mr-2" />
                <strong>Personalized Information Package</strong>
              </div>
              <div class="grid md:grid-cols-2 gap-4">
                <div class="bg-white border border-orange-200 rounded p-3">
                  <p class="font-medium text-orange-800 mb-2">Physical Mail Contents:</p>
                  <ul class="text-sm text-orange-700 space-y-1">
                    <li>• Personalized cover letter</li>
                    <li>• D&O coverage explanation</li>
                    <li>• Legal sector case studies</li>
                    <li>• Partnership protection benefits</li>
                  </ul>
                </div>
                <div class="bg-white border border-orange-200 rounded p-3">
                  <p class="font-medium text-orange-800 mb-2">Key Benefits Highlighted:</p>
                  <ul class="text-sm text-orange-700 space-y-1">
                    <li>• Partner personal asset protection</li>
                    <li>• Management liability coverage</li>
                    <li>• Legal defense cost coverage</li>
                    <li>• Regulatory investigation support</li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        {:else if currentStep === 5}
          <div class="mt-6 p-4 bg-nordic-50 rounded-lg">
            <div class="bg-green-50 border border-green-200 rounded-lg p-4">
              <div class="flex items-center mb-3">
                <Check class="h-6 w-6 text-green-600 mr-2" />
                <span class="font-semibold text-green-800">Successful Conversion!</span>
              </div>
              <div class="grid md:grid-cols-2 gap-4 text-sm">
                <div>
                  <strong class="text-green-800">Partnership Meeting Outcome:</strong>
                  <p class="text-green-700 mt-1">All 8 partners agreed on D&O importance after thorough discussion</p>
                </div>
                <div>
                  <strong class="text-green-800">D&O Coverage:</strong>
                  <p class="text-green-700 mt-1">€8,000/year premium for comprehensive partnership protection</p>
                </div>
              </div>
              <div class="mt-4 p-3 bg-white border border-green-200 rounded">
                <p class="font-medium text-green-800 mb-1">Key Success Factors:</p>
                <ul class="text-sm text-green-700 space-y-1">
                  <li>• Respected existing relationship</li>
                  <li>• No pressure sales approach</li>
                  <li>• Relevant legal sector focus</li>
                  <li>• Traditional communication preferences honored</li>
                </ul>
              </div>
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
    <h2 class="text-xl font-semibold text-nordic-800 mb-4">Human-Centric Approach Benefits</h2>
    
    <div class="grid md:grid-cols-2 gap-6">
      <div>
        <h4 class="font-medium text-nordic-800 mb-2">Relationship Preservation</h4>
        <ul class="text-nordic-600 text-sm space-y-1">
          <li>• 8-week gentle introduction process</li>
          <li>• No digital pressure tactics</li>
          <li>• Respected traditional communication preferences</li>
          <li>• Built on 15-year trusted relationship</li>
        </ul>
      </div>
      
      <div>
        <h4 class="font-medium text-nordic-800 mb-2">Targeted Expertise</h4>
        <ul class="text-nordic-600 text-sm space-y-1">
          <li>• Legal sector-specific risk analysis</li>
          <li>• Partnership structure understanding</li>
          <li>• Regulatory compliance focus</li>
          <li>• Professional liability expertise</li>
        </ul>
      </div>
    </div>
    
    <div class="mt-6 p-4 bg-nordic-50 rounded-lg">
      <p class="text-nordic-700 text-sm">
        <strong>Omni-Channel Insight:</strong> While this customer prefers traditional channels, 
        the system still coordinates across internal systems, CRM alerts, and human touchpoints 
        to ensure seamless experience and optimal timing.
      </p>
    </div>
  </div>
</div>
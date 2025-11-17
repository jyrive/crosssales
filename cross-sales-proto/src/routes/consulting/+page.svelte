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
    name: "Nordic Digital Consulting AB",
    employees: 12,
    industry: "Management Consulting",
    currentPolicies: ["Professional Indemnity", "General Liability"],
    incident: "Ransomware attack - 2 days downtime",
    customerType: "Digital-first",
    preferences: ["Email", "Self-service portal", "Mobile notifications", "Quick decisions"]
  };
  
  let journeySteps = [
    {
      hour: 2,
      title: "Incident Detection",
      channel: "News Monitoring",
      action: "Cyber incident detected via media monitoring",
      recommendation: "Immediate cyber insurance outreach",
      status: "triggered"
    },
    {
      hour: 6,
      title: "Automated Alert",
      channel: "Email",
      action: "Targeted cyber insurance email sent",
      recommendation: "Cyber coverage for digital consultancy risks",
      status: "sent"
    },
    {
      hour: 12,
      title: "Portal Engagement",
      channel: "MyBusiness Portal",
      action: "Customer logs in, sees cyber recommendation",
      recommendation: "Instant cyber quote: €5,200/year",
      status: "viewed"
    },
    {
      hour: 18,
      title: "Mobile Follow-up",
      channel: "SMS",
      action: "Mobile notification about cyber protection gap",
      recommendation: "Quick assessment link sent",
      status: "clicked"
    },
    {
      hour: 24,
      title: "Expert Consultation",
      channel: "Video Call",
      action: "Cyber specialist consultation scheduled",
      recommendation: "Comprehensive cyber package + business interruption",
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
      case 'News Monitoring': return Globe;
      case 'Email': return Mail;
      case 'MyBusiness Portal': return Globe;
      case 'SMS': return Phone;
      case 'Video Call': return Phone;
      default: return Globe;
    }
  }

  function getStatusColor(status) {
    switch(status) {
      case 'triggered': return 'bg-red-100 text-red-800';
      case 'sent': return 'bg-blue-100 text-blue-800';
      case 'viewed': return 'bg-yellow-100 text-yellow-800';
      case 'clicked': return 'bg-orange-100 text-orange-800';
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
        <Users class="h-8 w-8 text-primary-600 mr-3" />
        <div>
          <h1 class="text-2xl font-bold text-nordic-900">{companyData.name}</h1>
          <p class="text-nordic-600">Digital Consultancy - Reactive Cross-Sales After Cyber Incident</p>
        </div>
      </div>
      
      <div class="grid md:grid-cols-4 gap-4">
        <div class="flex items-center">
          <Users class="h-5 w-5 text-nordic-500 mr-2" />
          <span class="text-sm"><strong>{companyData.employees}</strong> employees</span>
        </div>
        <div class="flex items-center">
          <Shield class="h-5 w-5 text-nordic-500 mr-2" />
          <span class="text-sm"><strong>{companyData.currentPolicies.length}</strong> current policies</span>
        </div>
        <div class="flex items-center">
          <AlertTriangle class="h-5 w-5 text-red-500 mr-2" />
          <span class="text-sm"><strong>Cyber</strong> incident</span>
        </div>
        <div class="flex items-center">
          <Globe class="h-5 w-5 text-blue-500 mr-2" />
          <span class="text-sm"><strong>Digital</strong> first</span>
        </div>
      </div>
      
      <!-- Incident Alert -->
      <div class="mt-4 p-4 bg-red-50 border-l-4 border-red-500 rounded-r-lg">
        <div class="flex items-center">
          <AlertTriangle class="h-5 w-5 text-red-500 mr-2" />
          <span class="font-medium text-red-800">Recent Incident:</span>
          <span class="text-red-700 ml-2">{companyData.incident}</span>
        </div>
      </div>
    </div>
  </div>

  <!-- Journey Timeline -->
  <div class="bg-white rounded-lg shadow-md p-6 mb-8">
    <h2 class="text-xl font-semibold text-nordic-800 mb-6">Reactive 24-Hour Cross-Sales Response</h2>
    
    <!-- Progress Bar -->
    <div class="mb-8">
      <div class="flex justify-between mb-2">
        {#each journeySteps as step, index}
          <div class="flex flex-col items-center">
            <div class="w-8 h-8 rounded-full flex items-center justify-center text-xs font-medium
                        {index + 1 <= currentStep ? 'bg-primary-600 text-white' : 'bg-nordic-200 text-nordic-600'}">
              {step.hour}h
            </div>
            <span class="text-xs text-nordic-600 mt-1">{step.hour} hrs</span>
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
              <p class="text-nordic-600">{step.channel} • +{step.hour} hours after incident</p>
            </div>
          </div>
          <span class="px-3 py-1 rounded-full text-sm font-medium {getStatusColor(step.status)}">
            {step.status.charAt(0).toUpperCase() + step.status.slice(1)}
          </span>
        </div>
        
        <div class="grid md:grid-cols-2 gap-6">
          <div>
            <h4 class="font-medium text-nordic-800 mb-2">System Action</h4>
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
            <div class="bg-red-50 border border-red-200 rounded-lg p-4">
              <div class="flex items-center mb-2">
                <AlertTriangle class="h-5 w-5 text-red-600 mr-2" />
                <strong>Automated News Monitoring Alert</strong>
              </div>
              <div class="grid md:grid-cols-2 gap-4 text-sm">
                <div>
                  <p class="font-medium text-red-800 mb-1">Detected Event:</p>
                  <ul class="text-red-700 space-y-1">
                    <li>• Company: Nordic Digital Consulting AB</li>
                    <li>• Incident: Ransomware attack</li>
                    <li>• Impact: 2 days downtime</li>
                    <li>• Current coverage: No cyber insurance</li>
                  </ul>
                </div>
                <div>
                  <p class="font-medium text-red-800 mb-1">System Response:</p>
                  <ul class="text-red-700 space-y-1">
                    <li>• Trigger: Immediate cyber outreach</li>
                    <li>• Priority: High (recent incident)</li>
                    <li>• Approach: Empathetic support</li>
                    <li>• Timeline: 24-hour response window</li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        {:else if currentStep === 2}
          <div class="mt-6 p-4 bg-nordic-50 rounded-lg">
            <div class="bg-blue-50 border border-blue-200 rounded-lg p-4">
              <div class="flex items-center mb-3">
                <Mail class="h-5 w-5 text-blue-600 mr-2" />
                <strong>Empathetic Cyber Insurance Email</strong>
              </div>
              <div class="bg-white border border-blue-200 rounded p-3 text-sm">
                <p class="font-medium text-blue-800 mb-2">Subject: Support After Your Recent Cyber Challenge</p>
                <div class="space-y-2 text-blue-700">
                  <p>"We noticed the recent ransomware incident affecting your consultancy. We understand how disruptive this must have been for your team and clients."</p>
                  <p>"While we hope this never happens again, we'd like to help you prepare for future cyber risks with comprehensive cyber insurance coverage."</p>
                  <p><strong>Key Benefits Highlighted:</strong></p>
                  <ul class="ml-4 space-y-1">
                    <li>• Business interruption coverage for downtime</li>
                    <li>• Cyber forensics and recovery costs</li>
                    <li>• Client notification and credit monitoring</li>
                    <li>• Regulatory fine protection</li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        {:else if currentStep === 3}
          <div class="mt-6 p-4 bg-nordic-50 rounded-lg">
            <div class="bg-yellow-50 border border-yellow-200 rounded-lg p-4">
              <div class="flex items-center mb-3">
                <Globe class="h-5 w-5 text-yellow-600 mr-2" />
                <strong>MyBusiness Portal Recommendation</strong>
              </div>
              <div class="bg-white border border-yellow-200 rounded p-4">
                <div class="notification mb-4">
                  <div class="flex items-center">
                    <AlertTriangle class="h-5 w-5 text-primary-600 mr-2" />
                    <span class="font-medium">Cyber Protection Recommended</span>
                  </div>
                  <p class="mt-2">Based on recent industry incidents, we recommend cyber insurance for consulting firms handling sensitive client data.</p>
                </div>
                <div class="grid md:grid-cols-2 gap-3 text-sm">
                  <div class="bg-primary-50 rounded p-3">
                    <p class="font-medium text-primary-800">Cyber Insurance</p>
                    <p class="text-2xl font-bold text-primary-600">€5,200</p>
                    <p class="text-primary-700">Annual premium</p>
                    <button class="btn-primary w-full mt-2">Get Quote</button>
                  </div>
                  <div class="bg-primary-50 rounded p-3">
                    <p class="font-medium text-primary-800">Business Interruption</p>
                    <p class="text-2xl font-bold text-primary-600">€2,800</p>
                    <p class="text-primary-700">Additional coverage</p>
                    <button class="btn-secondary w-full mt-2">Learn More</button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        {:else if currentStep === 4}
          <div class="mt-6 p-4 bg-nordic-50 rounded-lg">
            <div class="bg-orange-50 border border-orange-200 rounded-lg p-4">
              <div class="flex items-center mb-3">
                <Phone class="h-5 w-5 text-orange-600 mr-2" />
                <strong>Mobile SMS Follow-up</strong>
              </div>
              <div class="bg-white border border-orange-200 rounded p-3">
                <div class="text-sm">
                  <p class="font-medium text-orange-800 mb-2">SMS Message:</p>
                  <div class="bg-orange-50 rounded p-3 border border-orange-200">
                    <p class="text-orange-800">
                      "Nordic Digital Consulting: After recent cyber challenges, assess your protection gap with our 2-min cyber risk calculator. Complete assessment → [link] Reply STOP to opt out."
                    </p>
                  </div>
                  <div class="mt-3 p-3 bg-green-50 border border-green-200 rounded">
                    <p class="text-sm text-green-700">
                      <strong>Result:</strong> Customer clicked link and completed risk assessment, showing high cyber exposure score.
                    </p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        {:else if currentStep === 5}
          <div class="mt-6 p-4 bg-nordic-50 rounded-lg">
            <div class="bg-green-50 border border-green-200 rounded-lg p-4">
              <div class="flex items-center mb-3">
                <Check class="h-6 w-6 text-green-600 mr-2" />
                <span class="font-semibold text-green-800">Expert Consultation & Conversion</span>
              </div>
              <div class="grid md:grid-cols-2 gap-4 text-sm">
                <div>
                  <strong class="text-green-800">Video Consultation Outcome:</strong>
                  <ul class="text-green-700 mt-1 space-y-1">
                    <li>• Cyber specialist reviewed recent incident</li>
                    <li>• Identified specific consulting firm risks</li>
                    <li>• Recommended comprehensive package</li>
                  </ul>
                </div>
                <div>
                  <strong class="text-green-800">Coverage Purchased:</strong>
                  <ul class="text-green-700 mt-1 space-y-1">
                    <li>• Cyber Insurance: €5,200/year</li>
                    <li>• Business Interruption: €2,800/year</li>
                    <li>• Total: €8,000/year additional premium</li>
                  </ul>
                </div>
              </div>
              <div class="mt-4 p-3 bg-white border border-green-200 rounded">
                <p class="font-medium text-green-800 mb-1">Reactive Cross-Sales Success Factors:</p>
                <ul class="text-sm text-green-700 space-y-1">
                  <li>• Immediate response within 2 hours of incident detection</li>
                  <li>• Empathetic approach acknowledging recent challenges</li>
                  <li>• Multi-channel engagement respecting digital preferences</li>
                  <li>• Expert consultation for technical cyber questions</li>
                  <li>• 24-hour conversion from incident to sale</li>
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
    <h2 class="text-xl font-semibold text-nordic-800 mb-4">Reactive Cross-Sales Benefits</h2>
    
    <div class="grid md:grid-cols-2 gap-6">
      <div>
        <h4 class="font-medium text-nordic-800 mb-2">Rapid Response Capability</h4>
        <ul class="text-nordic-600 text-sm space-y-1">
          <li>• Automated news monitoring and incident detection</li>
          <li>• 2-hour response time from incident to outreach</li>
          <li>• 24-hour conversion cycle</li>
          <li>• Real-time risk assessment tools</li>
        </ul>
      </div>
      
      <div>
        <h4 class="font-medium text-nordic-800 mb-2">Digital-First Engagement</h4>
        <ul class="text-nordic-600 text-sm space-y-1">
          <li>• Multi-channel digital touchpoints</li>
          <li>• Self-service risk assessment</li>
          <li>• Mobile-optimized experience</li>
          <li>• Expert video consultation when needed</li>
        </ul>
      </div>
    </div>
    
    <div class="mt-6 p-4 bg-nordic-50 rounded-lg">
      <p class="text-nordic-700 text-sm">
        <strong>Omni-Channel Intelligence:</strong> This reactive scenario demonstrates how the system 
        monitors external events, coordinates immediate multi-channel response, and adapts messaging 
        based on recent incidents while respecting customer's digital-first preferences.
      </p>
    </div>
  </div>
</div>
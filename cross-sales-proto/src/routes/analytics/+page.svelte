<script>
  import Building from '$lib/icons/Building.svelte';
  import Users from '$lib/icons/Users.svelte';
  import Shield from '$lib/icons/Shield.svelte';
  import AlertTriangle from '$lib/icons/AlertTriangle.svelte';
  import Check from '$lib/icons/Check.svelte';
  import ArrowLeft from '$lib/icons/ArrowLeft.svelte';
  import Target from '$lib/icons/Target.svelte';
  import Bolt from '$lib/icons/Bolt.svelte';
  import Mail from '$lib/icons/Mail.svelte';
  import Phone from '$lib/icons/Phone.svelte';
  import Globe from '$lib/icons/Globe.svelte';
  
  let selectedView = $state('journey');
  let selectedCustomer = $state('all');
  
  let journeyData = {
    all: {
      totalCustomers: 1247,
      completedJourneys: 893,
      avgTouchpoints: 4.2,
      conversionRate: 18.7,
      channels: [
        { name: 'Portal', usage: 89, effectiveness: 23, avgTime: '2.3 min' },
        { name: 'Email', usage: 78, effectiveness: 31, avgTime: '45 sec' },
        { name: 'SMS', usage: 34, effectiveness: 27, avgTime: '15 sec' },
        { name: 'Phone', usage: 52, effectiveness: 67, avgTime: '8.2 min' },
        { name: 'Physical Mail', usage: 12, effectiveness: 45, avgTime: '3.2 days' }
      ]
    },
    manufacturing: {
      totalCustomers: 423,
      completedJourneys: 312,
      avgTouchpoints: 3.8,
      conversionRate: 22.1,
      channels: [
        { name: 'Portal', usage: 94, effectiveness: 28, avgTime: '1.8 min' },
        { name: 'Email', usage: 87, effectiveness: 34, avgTime: '38 sec' },
        { name: 'SMS', usage: 41, effectiveness: 29, avgTime: '12 sec' },
        { name: 'Phone', usage: 67, effectiveness: 71, avgTime: '7.5 min' },
        { name: 'Physical Mail', usage: 8, effectiveness: 38, avgTime: '2.8 days' }
      ]
    },
    legal: {
      totalCustomers: 187,
      completedJourneys: 134,
      avgTouchpoints: 5.2,
      conversionRate: 16.8,
      channels: [
        { name: 'Portal', usage: 34, effectiveness: 12, avgTime: '4.1 min' },
        { name: 'Email', usage: 67, effectiveness: 23, avgTime: '1.2 min' },
        { name: 'SMS', usage: 12, effectiveness: 18, avgTime: '22 sec' },
        { name: 'Phone', usage: 89, effectiveness: 78, avgTime: '12.4 min' },
        { name: 'Physical Mail', usage: 67, effectiveness: 65, avgTime: '4.1 days' }
      ]
    },
    consulting: {
      totalCustomers: 298,
      completedJourneys: 267,
      avgTouchpoints: 3.1,
      conversionRate: 24.3,
      channels: [
        { name: 'Portal', usage: 96, effectiveness: 31, avgTime: '1.4 min' },
        { name: 'Email', usage: 89, effectiveness: 38, avgTime: '28 sec' },
        { name: 'SMS', usage: 72, effectiveness: 33, avgTime: '8 sec' },
        { name: 'Phone', usage: 23, effectiveness: 56, avgTime: '6.1 min' },
        { name: 'Physical Mail', usage: 3, effectiveness: 22, avgTime: '2.1 days' }
      ]
    }
  };

  let crossSalesFlow = [
    {
      step: 1,
      name: "Trigger Detection",
      customers: 1000,
      description: "Growth signals, renewals, external events",
      dropoff: 0
    },
    {
      step: 2,
      name: "Recommendation Generation",
      customers: 847,
      description: "ML engine creates personalized suggestions",
      dropoff: 15.3
    },
    {
      step: 3,
      name: "Channel Selection",
      customers: 742,
      description: "Optimal channel chosen based on preferences",
      dropoff: 12.4
    },
    {
      step: 4,
      name: "Initial Engagement",
      customers: 623,
      description: "First touchpoint delivered",
      dropoff: 16.0
    },
    {
      step: 5,
      name: "Follow-up Sequence",
      customers: 456,
      description: "Multi-channel nurturing campaign",
      dropoff: 26.8
    },
    {
      step: 6,
      name: "Human Handoff",
      customers: 298,
      description: "Expert consultation triggered",
      dropoff: 34.6
    },
    {
      step: 7,
      name: "Conversion",
      customers: 187,
      description: "Policy purchased",
      dropoff: 37.2
    }
  ];

  let performanceMetrics = [
    {
      metric: "Customer Satisfaction Score",
      current: 4.7,
      target: 4.5,
      trend: "+0.2",
      status: "positive"
    },
    {
      metric: "Time to First Engagement",
      current: "4.2 hours",
      target: "6 hours",
      trend: "-1.8h",
      status: "positive"
    },
    {
      metric: "Cross-Channel Consistency",
      current: "94.3%",
      target: "90%",
      trend: "+2.1%",
      status: "positive"
    },
    {
      metric: "Recommendation Accuracy",
      current: "87.6%",
      target: "85%",
      trend: "+1.4%",
      status: "positive"
    },
    {
      metric: "Channel Preference Prediction",
      current: "82.1%",
      target: "80%",
      trend: "-0.8%",
      status: "warning"
    },
    {
      metric: "Journey Completion Rate",
      current: "71.6%",
      target: "75%",
      trend: "-2.1%",
      status: "negative"
    }
  ];

  function getChannelIcon(channel) {
    switch(channel) {
      case 'Portal': return Globe;
      case 'Email': return Mail;
      case 'SMS': return Phone;
      case 'Phone': return Phone;
      case 'Physical Mail': return Mail;
      default: return Globe;
    }
  }

  function getStatusColor(status) {
    switch(status) {
      case 'positive': return 'text-green-600 bg-green-100';
      case 'warning': return 'text-yellow-600 bg-yellow-100';
      case 'negative': return 'text-red-600 bg-red-100';
      default: return 'text-gray-600 bg-gray-100';
    }
  }

  let currentJourneyData = $derived(journeyData[selectedCustomer]);
</script>

<div class="container mx-auto px-6 py-8">
  <!-- Header -->
  <div class="mb-8">
    <a href="/" class="inline-flex items-center text-primary-600 hover:text-primary-700 mb-4">
      <ArrowLeft class="h-4 w-4 mr-2" />
      Back to Scenarios
    </a>
    
    <div class="flex justify-between items-center">
      <div>
        <h1 class="text-3xl font-bold text-nordic-900">Journey Analytics & Performance</h1>
        <p class="text-nordic-600">Omni-channel customer journey insights and optimization</p>
      </div>
      
      <!-- View Selector -->
      <div class="flex bg-nordic-100 rounded-lg p-1">
        <button 
          onclick={() => selectedView = 'journey'} 
          class="px-4 py-2 rounded-md text-sm font-medium transition-colors
                 {selectedView === 'journey' ? 'bg-white text-primary-600 shadow-sm' : 'text-nordic-600 hover:text-primary-600'}">
          Journey Flow
        </button>
        <button 
          onclick={() => selectedView = 'channels'} 
          class="px-4 py-2 rounded-md text-sm font-medium transition-colors
                 {selectedView === 'channels' ? 'bg-white text-primary-600 shadow-sm' : 'text-nordic-600 hover:text-primary-600'}">
          Channel Analysis
        </button>
        <button 
          onclick={() => selectedView = 'performance'} 
          class="px-4 py-2 rounded-md text-sm font-medium transition-colors
                 {selectedView === 'performance' ? 'bg-white text-primary-600 shadow-sm' : 'text-nordic-600 hover:text-primary-600'}">
          Performance
        </button>
      </div>
    </div>
  </div>

  <!-- Customer Segment Filter -->
  <div class="mb-8 card">
    <div class="flex items-center justify-between">
      <h2 class="text-lg font-semibold text-nordic-800">Customer Segment Analysis</h2>
      <div class="flex bg-nordic-50 rounded-lg p-1">
        <button 
          onclick={() => selectedCustomer = 'all'} 
          class="px-3 py-2 rounded-md text-sm font-medium transition-colors
                 {selectedCustomer === 'all' ? 'bg-white text-primary-600 shadow-sm' : 'text-nordic-600 hover:text-primary-600'}">
          All Segments
        </button>
        <button 
          onclick={() => selectedCustomer = 'manufacturing'} 
          class="px-3 py-2 rounded-md text-sm font-medium transition-colors
                 {selectedCustomer === 'manufacturing' ? 'bg-white text-primary-600 shadow-sm' : 'text-nordic-600 hover:text-primary-600'}">
          Manufacturing
        </button>
        <button 
          onclick={() => selectedCustomer = 'legal'} 
          class="px-3 py-2 rounded-md text-sm font-medium transition-colors
                 {selectedCustomer === 'legal' ? 'bg-white text-primary-600 shadow-sm' : 'text-nordic-600 hover:text-primary-600'}">
          Legal Services
        </button>
        <button 
          onclick={() => selectedCustomer = 'consulting'} 
          class="px-3 py-2 rounded-md text-sm font-medium transition-colors
                 {selectedCustomer === 'consulting' ? 'bg-white text-primary-600 shadow-sm' : 'text-nordic-600 hover:text-primary-600'}">
          Consulting
        </button>
      </div>
    </div>
    
    <div class="grid md:grid-cols-4 gap-6 mt-6">
      <div class="text-center">
        <p class="text-3xl font-bold text-primary-600">{currentJourneyData.totalCustomers.toLocaleString()}</p>
        <p class="text-sm text-nordic-600">Total Customers</p>
      </div>
      <div class="text-center">
        <p class="text-3xl font-bold text-green-600">{currentJourneyData.completedJourneys.toLocaleString()}</p>
        <p class="text-sm text-nordic-600">Completed Journeys</p>
      </div>
      <div class="text-center">
        <p class="text-3xl font-bold text-blue-600">{currentJourneyData.avgTouchpoints}</p>
        <p class="text-sm text-nordic-600">Avg Touchpoints</p>
      </div>
      <div class="text-center">
        <p class="text-3xl font-bold text-orange-600">{currentJourneyData.conversionRate}%</p>
        <p class="text-sm text-nordic-600">Conversion Rate</p>
      </div>
    </div>
  </div>

  <!-- Dynamic Content Based on Selected View -->
  {#if selectedView === 'journey'}
    <!-- Cross-Sales Journey Flow -->
    <div class="card mb-8">
      <h2 class="text-xl font-semibold text-nordic-800 mb-6">Cross-Sales Journey Funnel Analysis</h2>
      
      <div class="space-y-6">
        {#each crossSalesFlow as step, index}
          <div class="flex items-center">
            <!-- Step Number -->
            <div class="flex-shrink-0 w-12 h-12 bg-primary-600 text-white rounded-full flex items-center justify-center font-bold mr-6">
              {step.step}
            </div>
            
            <!-- Step Details -->
            <div class="flex-1">
              <div class="flex justify-between items-center mb-2">
                <h4 class="font-semibold text-nordic-800">{step.name}</h4>
                <div class="flex items-center space-x-4">
                  <span class="text-2xl font-bold text-primary-600">{step.customers.toLocaleString()}</span>
                  {#if step.dropoff > 0}
                    <span class="text-sm text-red-600 bg-red-100 px-2 py-1 rounded">
                      -{step.dropoff}% dropoff
                    </span>
                  {/if}
                </div>
              </div>
              <p class="text-nordic-600 text-sm">{step.description}</p>
              
              <!-- Progress Bar -->
              <div class="w-full bg-nordic-200 rounded-full h-3 mt-3">
                <div class="bg-primary-600 h-3 rounded-full transition-all duration-500" 
                     style="width: {(step.customers / crossSalesFlow[0].customers) * 100}%"></div>
              </div>
            </div>
          </div>
          
          {#if index < crossSalesFlow.length - 1}
            <div class="flex justify-center">
              <div class="w-px h-8 bg-nordic-300"></div>
            </div>
          {/if}
        {/each}
      </div>
    </div>
    
  {:else if selectedView === 'channels'}
    <!-- Channel Performance Analysis -->
    <div class="card mb-8">
      <h2 class="text-xl font-semibold text-nordic-800 mb-6">Omni-Channel Performance Analysis</h2>
      
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
        {#each currentJourneyData.channels as channel}
          {@const ChannelIcon = getChannelIcon(channel.name)}
          <div class="bg-nordic-50 rounded-lg p-6">
            <div class="flex items-center mb-4">
              <div class="w-12 h-12 bg-white rounded-lg flex items-center justify-center mr-4">
                <ChannelIcon class="h-6 w-6 text-primary-600" />
              </div>
              <div>
                <h4 class="font-semibold text-nordic-800">{channel.name}</h4>
                <p class="text-sm text-nordic-600">Avg: {channel.avgTime}</p>
              </div>
            </div>
            
            <div class="space-y-3">
              <div>
                <div class="flex justify-between text-sm mb-1">
                  <span class="text-nordic-600">Usage Rate</span>
                  <span class="font-medium">{channel.usage}%</span>
                </div>
                <div class="w-full bg-nordic-200 rounded-full h-2">
                  <div class="bg-blue-600 h-2 rounded-full" style="width: {channel.usage}%"></div>
                </div>
              </div>
              
              <div>
                <div class="flex justify-between text-sm mb-1">
                  <span class="text-nordic-600">Effectiveness</span>
                  <span class="font-medium">{channel.effectiveness}%</span>
                </div>
                <div class="w-full bg-nordic-200 rounded-full h-2">
                  <div class="bg-green-600 h-2 rounded-full" style="width: {channel.effectiveness}%"></div>
                </div>
              </div>
            </div>
            
            <div class="mt-4 pt-4 border-t border-nordic-200">
              <p class="text-xs text-nordic-500">
                {#if channel.effectiveness > 50}
                  <span class="text-green-600">High performing channel</span>
                {:else if channel.effectiveness > 30}
                  <span class="text-yellow-600">Moderate performance</span>
                {:else}
                  <span class="text-red-600">Needs optimization</span>
                {/if}
              </p>
            </div>
          </div>
        {/each}
      </div>
    </div>
    
  {:else if selectedView === 'performance'}
    <!-- Performance Metrics -->
    <div class="card mb-8">
      <h2 class="text-xl font-semibold text-nordic-800 mb-6">Key Performance Indicators</h2>
      
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
        {#each performanceMetrics as metric}
          <div class="bg-nordic-50 rounded-lg p-6">
            <div class="flex justify-between items-start mb-3">
              <h4 class="font-medium text-nordic-800 text-sm">{metric.metric}</h4>
              <span class="px-2 py-1 rounded-full text-xs font-medium {getStatusColor(metric.status)}">
                {metric.trend}
              </span>
            </div>
            
            <div class="mb-2">
              <p class="text-2xl font-bold text-nordic-900">{metric.current}</p>
              <p class="text-sm text-nordic-600">Target: {metric.target}</p>
            </div>
            
            <div class="w-full bg-nordic-200 rounded-full h-2">
              <div class="bg-primary-600 h-2 rounded-full" style="width: 75%"></div>
            </div>
          </div>
        {/each}
      </div>
    </div>
  {/if}

  <!-- Insights and Recommendations -->
  <div class="grid lg:grid-cols-2 gap-8">
    
    <!-- Key Insights -->
    <div class="card">
      <h2 class="text-xl font-semibold text-nordic-800 mb-6">AI-Powered Insights</h2>
      
      <div class="space-y-4">
        <div class="p-4 bg-green-50 border border-green-200 rounded-lg">
          <div class="flex items-center mb-2">
            <Check class="h-5 w-5 text-green-600 mr-2" />
            <span class="font-medium text-green-800">High Performing Segment</span>
          </div>
          <p class="text-sm text-green-700">
            Consulting firms show 24.3% conversion rate, significantly above average. 
            Consider expanding digital-first approach to other segments.
          </p>
        </div>
        
        <div class="p-4 bg-yellow-50 border border-yellow-200 rounded-lg">
          <div class="flex items-center mb-2">
            <AlertTriangle class="h-5 w-5 text-yellow-600 mr-2" />
            <span class="font-medium text-yellow-800">Optimization Opportunity</span>
          </div>
          <p class="text-sm text-yellow-700">
            Legal services segment heavily relies on phone calls (89% usage). 
            Gradual digital adoption could improve efficiency.
          </p>
        </div>
        
        <div class="p-4 bg-blue-50 border border-blue-200 rounded-lg">
          <div class="flex items-center mb-2">
            <Target class="h-5 w-5 text-blue-600 mr-2" />
            <span class="font-medium text-blue-800">Cross-Channel Success</span>
          </div>
          <p class="text-sm text-blue-700">
            Customers engaging through 3+ channels show 67% higher conversion rates. 
            Current omni-channel strategy is effective.
          </p>
        </div>
      </div>
    </div>
    
    <!-- Recommendations -->
    <div class="card">
      <h2 class="text-xl font-semibold text-nordic-800 mb-6">Recommended Actions</h2>
      
      <div class="space-y-4">
        <div class="flex items-start p-4 bg-nordic-50 rounded-lg">
          <div class="w-8 h-8 bg-primary-600 text-white rounded-full flex items-center justify-center mr-4 mt-1">
            <span class="text-sm font-bold">1</span>
          </div>
          <div>
            <h4 class="font-medium text-nordic-800 mb-1">Enhance Email Personalization</h4>
            <p class="text-sm text-nordic-600">
              Increase email effectiveness from 31% to 40% through industry-specific messaging and dynamic content.
            </p>
          </div>
        </div>
        
        <div class="flex items-start p-4 bg-nordic-50 rounded-lg">
          <div class="w-8 h-8 bg-primary-600 text-white rounded-full flex items-center justify-center mr-4 mt-1">
            <span class="text-sm font-bold">2</span>
          </div>
          <div>
            <h4 class="font-medium text-nordic-800 mb-1">Reduce Journey Dropoff</h4>
            <p class="text-sm text-nordic-600">
              Focus on step 5-6 transition where 34.6% dropoff occurs. Implement smart timing algorithms for human handoff.
            </p>
          </div>
        </div>
        
        <div class="flex items-start p-4 bg-nordic-50 rounded-lg">
          <div class="w-8 h-8 bg-primary-600 text-white rounded-full flex items-center justify-center mr-4 mt-1">
            <span class="text-sm font-bold">3</span>
          </div>
          <div>
            <h4 class="font-medium text-nordic-800 mb-1">Expand SMS Usage</h4>
            <p class="text-sm text-nordic-600">
              SMS shows good effectiveness (27%) but low usage (34%). Test opt-in campaigns for immediate notifications.
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
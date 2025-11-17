<script>
  import Building from '$lib/icons/Building.svelte';
  import Users from '$lib/icons/Users.svelte';
  import Shield from '$lib/icons/Shield.svelte';
  import AlertTriangle from '$lib/icons/AlertTriangle.svelte';
  import Check from '$lib/icons/Check.svelte';
  import ArrowLeft from '$lib/icons/ArrowLeft.svelte';
  import Target from '$lib/icons/Target.svelte';
  import Bolt from '$lib/icons/Bolt.svelte';
  
  let selectedTimeframe = $state('today');
  
  let dashboardData = {
    today: {
      recommendations: 47,
      conversions: 8,
      revenue: 42800,
      conversionRate: 17.0,
      activeCustomers: 312,
      campaigns: 12
    },
    week: {
      recommendations: 284,
      conversions: 52,
      revenue: 267500,
      conversionRate: 18.3,
      activeCustomers: 1847,
      campaigns: 28
    },
    month: {
      recommendations: 1205,
      conversions: 218,
      revenue: 1134600,
      conversionRate: 18.1,
      activeCustomers: 5623,
      campaigns: 67
    }
  };
  
  let recentActivities = [
    {
      time: "2 minutes ago",
      type: "conversion",
      customer: "Nordic Manufacturing AB",
      action: "Purchased Workers' Comp + Product Liability",
      value: "€9,100"
    },
    {
      time: "8 minutes ago", 
      type: "recommendation",
      customer: "Bergström Law Firm",
      action: "D&O recommendation sent via email",
      value: "€8,000"
    },
    {
      time: "15 minutes ago",
      type: "trigger",
      customer: "Digital Consulting AB",
      action: "Cyber incident detected - outreach initiated",
      value: "€5,200"
    },
    {
      time: "23 minutes ago",
      type: "engagement",
      customer: "Tech Solutions AS",
      action: "Portal notification viewed",
      value: "€3,400"
    },
    {
      time: "31 minutes ago",
      type: "conversion",
      customer: "Nordic Logistics Oy",
      action: "Cargo insurance added to existing policy",
      value: "€4,800"
    }
  ];
  
  let topRecommendations = [
    { product: "Cyber Insurance", opportunities: 89, conversionRate: 22, avgValue: 5200 },
    { product: "Workers' Compensation", opportunities: 67, conversionRate: 31, avgValue: 4200 },
    { product: "D&O Coverage", opportunities: 45, conversionRate: 16, avgValue: 8000 },
    { product: "Product Liability", opportunities: 38, conversionRate: 28, avgValue: 3100 },
    { product: "Business Interruption", opportunities: 31, conversionRate: 19, avgValue: 6800 }
  ];

  function getActivityIcon(type) {
    switch(type) {
      case 'conversion': return Check;
      case 'recommendation': return Target;
      case 'trigger': return AlertTriangle;
      case 'engagement': return Users;
      default: return Building;
    }
  }

  function getActivityColor(type) {
    switch(type) {
      case 'conversion': return 'text-green-600';
      case 'recommendation': return 'text-blue-600';
      case 'trigger': return 'text-orange-600';
      case 'engagement': return 'text-purple-600';
      default: return 'text-gray-600';
    }
  }

  let currentData = $derived(dashboardData[selectedTimeframe]);
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
        <h1 class="text-3xl font-bold text-nordic-900">Cross-Sales Admin Dashboard</h1>
        <p class="text-nordic-600">Real-time monitoring and analytics</p>
      </div>
      
      <!-- Timeframe Selector -->
      <div class="flex bg-nordic-100 rounded-lg p-1">
        <button 
          onclick={() => selectedTimeframe = 'today'} 
          class="px-4 py-2 rounded-md text-sm font-medium transition-colors
                 {selectedTimeframe === 'today' ? 'bg-white text-primary-600 shadow-sm' : 'text-nordic-600 hover:text-primary-600'}">
          Today
        </button>
        <button 
          onclick={() => selectedTimeframe = 'week'} 
          class="px-4 py-2 rounded-md text-sm font-medium transition-colors
                 {selectedTimeframe === 'week' ? 'bg-white text-primary-600 shadow-sm' : 'text-nordic-600 hover:text-primary-600'}">
          This Week
        </button>
        <button 
          onclick={() => selectedTimeframe = 'month'} 
          class="px-4 py-2 rounded-md text-sm font-medium transition-colors
                 {selectedTimeframe === 'month' ? 'bg-white text-primary-600 shadow-sm' : 'text-nordic-600 hover:text-primary-600'}">
          This Month
        </button>
      </div>
    </div>
  </div>

  <!-- Key Metrics -->
  <div class="grid md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-6 gap-6 mb-8">
    <div class="card">
      <div class="flex items-center">
        <Target class="h-8 w-8 text-primary-600 mr-3" />
        <div>
          <p class="text-sm text-nordic-600">Recommendations</p>
          <p class="text-2xl font-bold text-nordic-900">{currentData.recommendations}</p>
        </div>
      </div>
    </div>
    
    <div class="card">
      <div class="flex items-center">
        <Check class="h-8 w-8 text-green-600 mr-3" />
        <div>
          <p class="text-sm text-nordic-600">Conversions</p>
          <p class="text-2xl font-bold text-nordic-900">{currentData.conversions}</p>
        </div>
      </div>
    </div>
    
    <div class="card">
      <div class="flex items-center">
        <Bolt class="h-8 w-8 text-primary-600 mr-3" />
        <div>
          <p class="text-sm text-nordic-600">Revenue</p>
          <p class="text-2xl font-bold text-nordic-900">€{currentData.revenue.toLocaleString()}</p>
        </div>
      </div>
    </div>
    
    <div class="card">
      <div class="flex items-center">
        <Target class="h-8 w-8 text-orange-600 mr-3" />
        <div>
          <p class="text-sm text-nordic-600">Conv. Rate</p>
          <p class="text-2xl font-bold text-nordic-900">{currentData.conversionRate}%</p>
        </div>
      </div>
    </div>
    
    <div class="card">
      <div class="flex items-center">
        <Users class="h-8 w-8 text-blue-600 mr-3" />
        <div>
          <p class="text-sm text-nordic-600">Active Customers</p>
          <p class="text-2xl font-bold text-nordic-900">{currentData.activeCustomers}</p>
        </div>
      </div>
    </div>
    
    <div class="card">
      <div class="flex items-center">
        <Building class="h-8 w-8 text-purple-600 mr-3" />
        <div>
          <p class="text-sm text-nordic-600">Campaigns</p>
          <p class="text-2xl font-bold text-nordic-900">{currentData.campaigns}</p>
        </div>
      </div>
    </div>
  </div>

  <!-- Main Content Grid -->
  <div class="grid lg:grid-cols-3 gap-8">
    
    <!-- Recent Activity Feed -->
    <div class="lg:col-span-2 card">
      <h2 class="text-xl font-semibold text-nordic-800 mb-6">Real-Time Activity Feed</h2>
      <div class="space-y-4">
        {#each recentActivities as activity}
          {@const ActivityIcon = getActivityIcon(activity.type)}
          <div class="flex items-center p-4 bg-nordic-50 rounded-lg">
            <div class="flex-shrink-0 w-10 h-10 bg-white rounded-full flex items-center justify-center mr-4">
              <ActivityIcon class="h-5 w-5 {getActivityColor(activity.type)}" />
            </div>
            <div class="flex-1">
              <div class="flex justify-between items-start">
                <div>
                  <p class="font-medium text-nordic-800">{activity.customer}</p>
                  <p class="text-sm text-nordic-600">{activity.action}</p>
                  <p class="text-xs text-nordic-500">{activity.time}</p>
                </div>
                <span class="text-sm font-semibold text-green-600">{activity.value}</span>
              </div>
            </div>
          </div>
        {/each}
      </div>
    </div>

    <!-- Top Recommendations -->
    <div class="card">
      <h2 class="text-xl font-semibold text-nordic-800 mb-6">Top Performing Products</h2>
      <div class="space-y-4">
        {#each topRecommendations as product}
          <div class="p-4 bg-nordic-50 rounded-lg">
            <div class="flex justify-between items-center mb-2">
              <h4 class="font-medium text-nordic-800">{product.product}</h4>
              <span class="text-xs bg-primary-100 text-primary-700 px-2 py-1 rounded">
                {product.conversionRate}% conv.
              </span>
            </div>
            <div class="text-sm text-nordic-600">
              <p>{product.opportunities} opportunities</p>
              <p class="font-semibold text-primary-600">€{product.avgValue.toLocaleString()} avg. value</p>
            </div>
            <div class="w-full bg-nordic-200 rounded-full h-2 mt-3">
              <div class="bg-primary-600 h-2 rounded-full" style="width: {product.conversionRate}%"></div>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </div>

  <!-- System Health Status -->
  <div class="card mt-8">
    <h2 class="text-xl font-semibold text-nordic-800 mb-6">System Status & Health</h2>
    <div class="grid md:grid-cols-4 gap-6">
      <div class="text-center">
        <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-3">
          <Check class="h-8 w-8 text-green-600" />
        </div>
        <h4 class="font-medium text-nordic-800">Data Pipeline</h4>
        <p class="text-sm text-green-600">Operational</p>
        <p class="text-xs text-nordic-500">Last sync: 2 min ago</p>
      </div>
      
      <div class="text-center">
        <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-3">
          <Bolt class="h-8 w-8 text-green-600" />
        </div>
        <h4 class="font-medium text-nordic-800">ML Engine</h4>
        <p class="text-sm text-green-600">Running</p>
        <p class="text-xs text-nordic-500">Models updated: 1 hour ago</p>
      </div>
      
      <div class="text-center">
        <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-3">
          <Target class="h-8 w-8 text-green-600" />
        </div>
        <h4 class="font-medium text-nordic-800">Recommendations</h4>
        <p class="text-sm text-green-600">Active</p>
        <p class="text-xs text-nordic-500">Processing: 47 queued</p>
      </div>
      
      <div class="text-center">
        <div class="w-16 h-16 bg-yellow-100 rounded-full flex items-center justify-center mx-auto mb-3">
          <AlertTriangle class="h-8 w-8 text-yellow-600" />
        </div>
        <h4 class="font-medium text-nordic-800">External APIs</h4>
        <p class="text-sm text-yellow-600">Degraded</p>
        <p class="text-xs text-nordic-500">News feed: 15s delay</p>
      </div>
    </div>
  </div>
</div>
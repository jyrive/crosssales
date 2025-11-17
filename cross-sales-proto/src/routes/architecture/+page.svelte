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
  
  let selectedComponent = $state('overview');
  
  let components = [
    {
      id: 'data-aggregation',
      name: 'Data Aggregation Layer',
      description: 'Collects and normalizes data from multiple sources',
      technology: 'Azure Data Factory, Event Hubs',
      connections: ['customer-intelligence', 'external-data'],
      features: [
        'Real-time policy data sync',
        'Customer behavior tracking', 
        'External market data integration',
        'GDPR-compliant data processing'
      ],
      status: 'operational',
      position: { x: 10, y: 20 }
    },
    {
      id: 'customer-intelligence',
      name: 'Customer Intelligence Engine',
      description: 'AI-powered customer analysis and risk profiling',
      technology: 'Azure ML, Databricks, Python',
      connections: ['cross-sales-engine', 'data-aggregation'],
      features: [
        'Behavioral pattern analysis',
        'Risk profile generation',
        'Life event detection',
        'Propensity scoring'
      ],
      status: 'operational',
      position: { x: 35, y: 20 }
    },
    {
      id: 'cross-sales-engine',
      name: 'Cross-Sales Recommendation Engine',
      description: 'Generates personalized product recommendations',
      technology: 'Azure ML, Custom Algorithms',
      connections: ['next-best-action', 'customer-intelligence'],
      features: [
        'ML-based product matching',
        'Coverage gap analysis',
        'Competitive pricing logic',
        'Business rules engine'
      ],
      status: 'operational',
      position: { x: 60, y: 20 }
    },
    {
      id: 'next-best-action',
      name: 'Next Best Action Engine',
      description: 'Determines optimal engagement strategy',
      technology: 'Azure Logic Apps, Custom APIs',
      connections: ['decision-orchestrator', 'cross-sales-engine'],
      features: [
        'Channel preference prediction',
        'Timing optimization',
        'Message personalization',
        'Journey orchestration'
      ],
      status: 'operational',
      position: { x: 85, y: 20 }
    },
    {
      id: 'decision-orchestrator',
      name: 'Decision Orchestrator',
      description: 'Coordinates campaign execution and resource allocation',
      technology: 'Azure Service Bus, Logic Apps',
      connections: ['delivery-engine', 'next-best-action'],
      features: [
        'Campaign coordination',
        'Resource allocation',
        'Priority management',
        'Conflict resolution'
      ],
      status: 'operational',
      position: { x: 60, y: 60 }
    },
    {
      id: 'delivery-engine',
      name: 'Omni-Channel Delivery Engine',
      description: 'Executes multi-channel customer engagement',
      technology: 'Salesforce, Azure Communication Services',
      connections: ['customer-touchpoints', 'decision-orchestrator'],
      features: [
        'Email campaign execution',
        'SMS notifications',
        'Portal recommendations',
        'Human handoff triggers'
      ],
      status: 'operational',
      position: { x: 35, y: 60 }
    },
    {
      id: 'customer-touchpoints',
      name: 'Customer Touchpoints',
      description: 'Direct customer interaction channels',
      technology: 'MyBusiness Portal, Salesforce CRM',
      connections: ['delivery-engine'],
      features: [
        'MyBusiness self-service portal',
        'Digital webshop integration',
        'Call center systems',
        'Email/SMS delivery'
      ],
      status: 'operational',
      position: { x: 10, y: 60 }
    },
    {
      id: 'external-data',
      name: 'External Data Sources',
      description: 'Third-party data feeds and market intelligence',
      technology: 'REST APIs, Azure Data Factory',
      connections: ['data-aggregation'],
      features: [
        'Industry news monitoring',
        'Market data feeds',
        'Credit scoring services',
        'Business registry data'
      ],
      status: 'operational',
      position: { x: 10, y: 5 }
    }
  ];

  let integrationPoints = [
    {
      name: 'Salesforce CRM',
      type: 'Primary System',
      description: 'Customer relationship management and policy data',
      apis: ['REST API', 'Bulk API', 'Streaming API'],
      dataFlow: 'Bidirectional',
      status: 'connected'
    },
    {
      name: 'MyBusiness Portal',
      type: 'Customer Interface',
      description: 'Self-service customer portal with recommendation widgets',
      apis: ['REST API', 'GraphQL'],
      dataFlow: 'Bidirectional',
      status: 'connected'
    },
    {
      name: 'Azure Databricks',
      type: 'Analytics Platform',
      description: 'Advanced analytics and machine learning workloads',
      apis: ['Databricks API', 'JDBC/ODBC'],
      dataFlow: 'Inbound',
      status: 'connected'
    },
    {
      name: 'Azure Data Factory',
      type: 'ETL Platform',
      description: 'Data integration and transformation services',
      apis: ['REST API', 'PowerShell'],
      dataFlow: 'Orchestration',
      status: 'connected'
    },
    {
      name: 'Azure Communication Services',
      type: 'Communication Platform',
      description: 'Email, SMS, and calling capabilities',
      apis: ['REST API', 'SDKs'],
      dataFlow: 'Outbound',
      status: 'connected'
    },
    {
      name: 'External News APIs',
      type: 'Data Feed',
      description: 'Real-time industry news and incident monitoring',
      apis: ['REST API', 'Webhooks'],
      dataFlow: 'Inbound',
      status: 'connected'
    }
  ];

  let dataFlow = [
    {
      source: 'Customer Portal',
      target: 'Data Aggregation',
      data: 'User interactions, profile updates',
      volume: '~1,200 events/hour',
      latency: '< 100ms'
    },
    {
      source: 'Salesforce CRM',
      target: 'Data Aggregation',
      data: 'Policy data, customer information',
      volume: '~850 updates/hour',
      latency: '< 2 seconds'
    },
    {
      source: 'Data Aggregation',
      target: 'Customer Intelligence',
      data: 'Normalized customer data',
      volume: '~2,000 records/hour',
      latency: '< 5 seconds'
    },
    {
      source: 'Customer Intelligence',
      target: 'Cross-Sales Engine',
      data: 'Risk profiles, behavioral insights',
      volume: '~500 analyses/hour',
      latency: '< 30 seconds'
    },
    {
      source: 'Cross-Sales Engine',
      target: 'Next Best Action',
      data: 'Product recommendations',
      volume: '~300 recommendations/hour',
      latency: '< 10 seconds'
    }
  ];

  function getComponentById(id) {
    return components.find(c => c.id === id) || components[0];
  }

  function getStatusColor(status) {
    switch(status) {
      case 'operational': return 'text-green-600 bg-green-100';
      case 'warning': return 'text-yellow-600 bg-yellow-100';
      case 'error': return 'text-red-600 bg-red-100';
      default: return 'text-gray-600 bg-gray-100';
    }
  }

  function getDataFlowColor(latency) {
    if (latency.includes('100ms')) return 'text-green-600';
    if (latency.includes('seconds') && !latency.includes('30')) return 'text-blue-600';
    return 'text-orange-600';
  }

  let selectedComponentDetails = $derived(getComponentById(selectedComponent));
</script>

<div class="container mx-auto px-6 py-8">
  <!-- Header -->
  <div class="mb-8">
    <a href="/" class="inline-flex items-center text-primary-600 hover:text-primary-700 mb-4">
      <ArrowLeft class="h-4 w-4 mr-2" />
      Back to Scenarios
    </a>
    
    <div>
      <h1 class="text-3xl font-bold text-nordic-900">System Architecture Overview</h1>
      <p class="text-nordic-600">Interactive view of cross-sales system components and data flows</p>
    </div>
  </div>

  <!-- Architecture Diagram -->
  <div class="card mb-8">
    <h2 class="text-xl font-semibold text-nordic-800 mb-6">Logical Architecture Components</h2>
    
    <div class="relative bg-gradient-to-br from-blue-50 to-purple-50 rounded-lg p-8 min-h-[500px] overflow-hidden">
      <!-- Background Grid -->
      <div class="absolute inset-0 opacity-20">
        <svg width="100%" height="100%">
          <defs>
            <pattern id="grid" width="40" height="40" patternUnits="userSpaceOnUse">
              <path d="M 40 0 L 0 0 0 40" fill="none" stroke="#e5e7eb" stroke-width="1"/>
            </pattern>
          </defs>
          <rect width="100%" height="100%" fill="url(#grid)" />
        </svg>
      </div>
      
      <!-- Components -->
      {#each components as component}
        <button 
          class="absolute transform -translate-x-1/2 -translate-y-1/2 cursor-pointer focus:outline-none"
          style="left: {component.position.x}%; top: {component.position.y}%"
          onclick={() => selectedComponent = component.id}>
          <div class="bg-white rounded-lg shadow-lg p-4 border-2 transition-all duration-200
                      {selectedComponent === component.id ? 'border-primary-500 shadow-xl' : 'border-gray-200 hover:border-primary-300'}
                      max-w-[200px]">
            <div class="flex items-center mb-2">
              <Building class="h-5 w-5 text-primary-600 mr-2" />
              <span class="px-2 py-1 rounded-full text-xs font-medium {getStatusColor(component.status)}">
                {component.status}
              </span>
            </div>
            <h4 class="font-semibold text-nordic-800 text-sm mb-1">{component.name}</h4>
            <p class="text-xs text-nordic-600">{component.description}</p>
          </div>
        </button>
      {/each}
      
      <!-- Connection Lines (simplified) -->
      <svg class="absolute inset-0 pointer-events-none">
        <defs>
          <marker id="arrowhead" markerWidth="10" markerHeight="7" refX="10" refY="3.5" orient="auto">
            <polygon points="0 0, 10 3.5, 0 7" fill="#6b7280" />
          </marker>
        </defs>
        <!-- Example connections - in a real app, these would be calculated dynamically -->
        <line x1="20%" y1="25%" x2="35%" y2="25%" stroke="#6b7280" stroke-width="2" opacity="0.6" marker-end="url(#arrowhead)" />
        <line x1="50%" y1="25%" x2="60%" y2="25%" stroke="#6b7280" stroke-width="2" opacity="0.6" marker-end="url(#arrowhead)" />
        <line x1="75%" y1="25%" x2="85%" y2="25%" stroke="#6b7280" stroke-width="2" opacity="0.6" marker-end="url(#arrowhead)" />
        <line x1="80%" y1="30%" x2="70%" y2="55%" stroke="#6b7280" stroke-width="2" opacity="0.6" marker-end="url(#arrowhead)" />
        <line x1="55%" y1="65%" x2="40%" y2="65%" stroke="#6b7280" stroke-width="2" opacity="0.6" marker-end="url(#arrowhead)" />
        <line x1="30%" y1="65%" x2="20%" y2="65%" stroke="#6b7280" stroke-width="2" opacity="0.6" marker-end="url(#arrowhead)" />
      </svg>
    </div>
  </div>

  <!-- Component Details -->
  <div class="grid lg:grid-cols-3 gap-8 mb-8">
    
    <!-- Selected Component Details -->
    <div class="lg:col-span-2 card">
      <div class="flex items-center justify-between mb-6">
        <h2 class="text-xl font-semibold text-nordic-800">Component Details</h2>
        <span class="px-3 py-1 rounded-full text-sm font-medium {getStatusColor(selectedComponentDetails.status)}">
          {selectedComponentDetails.status}
        </span>
      </div>
      
      <div class="mb-6">
        <h3 class="text-lg font-semibold text-nordic-800 mb-2">{selectedComponentDetails.name}</h3>
        <p class="text-nordic-600 mb-4">{selectedComponentDetails.description}</p>
        <p class="text-sm text-nordic-500">
          <strong>Technology Stack:</strong> {selectedComponentDetails.technology}
        </p>
      </div>
      
      <div class="grid md:grid-cols-2 gap-6">
        <div>
          <h4 class="font-medium text-nordic-800 mb-3">Key Features</h4>
          <ul class="space-y-2">
            {#each selectedComponentDetails.features as feature}
              <li class="flex items-center text-sm text-nordic-600">
                <Check class="h-4 w-4 text-green-600 mr-2 flex-shrink-0" />
                {feature}
              </li>
            {/each}
          </ul>
        </div>
        
        <div>
          <h4 class="font-medium text-nordic-800 mb-3">Connected Components</h4>
          <div class="space-y-2">
            {#each selectedComponentDetails.connections as connectionId}
              {@const connectedComponent = getComponentById(connectionId)}
              <button 
                onclick={() => selectedComponent = connectionId}
                class="block w-full text-left p-2 bg-nordic-50 hover:bg-primary-50 rounded-lg transition-colors">
                <p class="text-sm font-medium text-nordic-800">{connectedComponent.name}</p>
                <p class="text-xs text-nordic-600">{connectedComponent.description}</p>
              </button>
            {/each}
          </div>
        </div>
      </div>
    </div>
    
    <!-- Quick Component Navigator -->
    <div class="card">
      <h2 class="text-xl font-semibold text-nordic-800 mb-6">Component Navigator</h2>
      
      <div class="space-y-3">
        {#each components as component}
          <button 
            onclick={() => selectedComponent = component.id}
            class="block w-full text-left p-3 rounded-lg transition-colors
                   {selectedComponent === component.id ? 'bg-primary-100 border-primary-300' : 'bg-nordic-50 hover:bg-nordic-100'}">
            <div class="flex items-center justify-between mb-1">
              <p class="text-sm font-medium text-nordic-800">{component.name}</p>
              <span class="w-2 h-2 rounded-full {component.status === 'operational' ? 'bg-green-500' : 'bg-yellow-500'}"></span>
            </div>
            <p class="text-xs text-nordic-600">{component.description}</p>
          </button>
        {/each}
      </div>
    </div>
  </div>

  <!-- Integration Points & Data Flow -->
  <div class="grid lg:grid-cols-2 gap-8">
    
    <!-- Integration Points -->
    <div class="card">
      <h2 class="text-xl font-semibold text-nordic-800 mb-6">Integration Points</h2>
      
      <div class="space-y-4">
        {#each integrationPoints as integration}
          <div class="p-4 bg-nordic-50 rounded-lg">
            <div class="flex items-center justify-between mb-2">
              <div>
                <h4 class="font-semibold text-nordic-800">{integration.name}</h4>
                <p class="text-sm text-nordic-600">{integration.type}</p>
              </div>
              <span class="px-2 py-1 rounded-full text-xs bg-green-100 text-green-800">
                {integration.status}
              </span>
            </div>
            <p class="text-sm text-nordic-600 mb-2">{integration.description}</p>
            <div class="flex justify-between text-xs text-nordic-500">
              <span>APIs: {integration.apis.join(', ')}</span>
              <span>Data Flow: {integration.dataFlow}</span>
            </div>
          </div>
        {/each}
      </div>
    </div>
    
    <!-- Data Flow -->
    <div class="card">
      <h2 class="text-xl font-semibold text-nordic-800 mb-6">Data Flow Analysis</h2>
      
      <div class="space-y-4">
        {#each dataFlow as flow}
          <div class="p-4 bg-nordic-50 rounded-lg">
            <div class="flex items-center mb-2">
              <span class="text-sm font-medium text-nordic-800">{flow.source}</span>
              <ArrowLeft class="h-4 w-4 text-nordic-400 mx-2 transform rotate-180" />
              <span class="text-sm font-medium text-nordic-800">{flow.target}</span>
            </div>
            <p class="text-sm text-nordic-600 mb-2">{flow.data}</p>
            <div class="grid grid-cols-2 gap-4 text-xs">
              <div>
                <span class="text-nordic-500">Volume:</span>
                <span class="font-medium text-nordic-700">{flow.volume}</span>
              </div>
              <div>
                <span class="text-nordic-500">Latency:</span>
                <span class="font-medium {getDataFlowColor(flow.latency)}">{flow.latency}</span>
              </div>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </div>
</div>
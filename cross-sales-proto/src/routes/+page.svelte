<script>
  import Building from '$lib/icons/Building.svelte';
  import Shield from '$lib/icons/Shield.svelte';
  import Users from '$lib/icons/Users.svelte';
  import ArrowRight from '$lib/icons/ArrowRight.svelte';
  import Bolt from '$lib/icons/Bolt.svelte';
  import Target from '$lib/icons/Target.svelte';
</script>

<div class="container mx-auto px-6 py-12">
  <!-- Header -->
  <div class="text-center mb-16">
    <h1 class="text-4xl font-bold text-nordic-900 mb-4">
      Cross-Sales Insurance Prototype
    </h1>
    <p class="text-xl text-nordic-600 max-w-3xl mx-auto">
      Interactive demos showcasing omni-channel cross-sales experiences for Nordic B2B insurance customers
    </p>
  </div>

  <!-- Scenario Cards -->
  <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8 mb-16">
    
    <!-- Manufacturing Company Scenario -->
    <a href="/manufacturing" class="recommendation-card group">
      <div class="flex items-center mb-4">
        <Building class="h-8 w-8 text-primary-600 mr-3" />
        <h3 class="text-xl font-semibold text-nordic-800">Manufacturing Company</h3>
      </div>
      <p class="text-nordic-600 mb-4">
        Growing tech manufacturer expanding workforce. Demonstrates progression from General Liability to Workers' Comp and Product Liability coverage.
      </p>
      <div class="flex items-center text-primary-600 group-hover:text-primary-700 font-medium">
        View Demo <ArrowRight class="h-4 w-4 ml-2" />
      </div>
    </a>

    <!-- Law Firm Scenario -->
    <a href="/lawfirm" class="recommendation-card group">
      <div class="flex items-center mb-4">
        <Shield class="h-8 w-8 text-primary-600 mr-3" />
        <h3 class="text-xl font-semibold text-nordic-800">Law Firm</h3>
      </div>
      <p class="text-nordic-600 mb-4">
        Traditional service company with Professional Indemnity. Shows human-centric approach to introducing D&O coverage.
      </p>
      <div class="flex items-center text-primary-600 group-hover:text-primary-700 font-medium">
        View Demo <ArrowRight class="h-4 w-4 ml-2" />
      </div>
    </a>

    <!-- Consulting Firm Scenario -->
    <a href="/consulting" class="recommendation-card group">
      <div class="flex items-center mb-4">
        <Users class="h-8 w-8 text-primary-600 mr-3" />
        <h3 class="text-xl font-semibold text-nordic-800">Consulting Firm</h3>
      </div>
      <p class="text-nordic-600 mb-4">
        Digital-first consultancy after cyber incident. Demonstrates reactive cross-sales and omni-channel engagement.
      </p>
      <div class="flex items-center text-primary-600 group-hover:text-primary-700 font-medium">
        View Demo <ArrowRight class="h-4 w-4 ml-2" />
      </div>
    </a>

    <!-- Admin Dashboard -->
    <a href="/admin" class="card group border-2 border-dashed border-nordic-300 hover:border-primary-400">
      <div class="flex items-center mb-4">
        <Bolt class="h-8 w-8 text-nordic-500 mr-3" />
        <h3 class="text-xl font-semibold text-nordic-700">Admin Dashboard</h3>
      </div>
      <p class="text-nordic-600 mb-4">
        Internal view of cross-sales engine, recommendation analytics, and campaign performance.
      </p>
      <div class="flex items-center text-nordic-600 group-hover:text-primary-600 font-medium">
        View Dashboard <ArrowRight class="h-4 w-4 ml-2" />
      </div>
    </a>

    <!-- Journey Analytics -->
    <a href="/analytics" class="card group border-2 border-dashed border-nordic-300 hover:border-primary-400">
      <div class="flex items-center mb-4">
        <Target class="h-8 w-8 text-nordic-500 mr-3" />
        <h3 class="text-xl font-semibold text-nordic-700">Journey Analytics</h3>
      </div>
      <p class="text-nordic-600 mb-4">
        Omni-channel customer journey visualization and cross-sales performance metrics.
      </p>
      <div class="flex items-center text-nordic-600 group-hover:text-primary-600 font-medium">
        View Analytics <ArrowRight class="h-4 w-4 ml-2" />
      </div>
    </a>

    <!-- System Architecture -->
    <a href="/architecture" class="card group border-2 border-dashed border-nordic-300 hover:border-primary-400">
      <div class="flex items-center mb-4">
        <Building class="h-8 w-8 text-nordic-500 mr-3" />
        <h3 class="text-xl font-semibold text-nordic-700">System Architecture</h3>
      </div>
      <p class="text-nordic-600 mb-4">
        Interactive view of logical components, data flows, and integration points.
      </p>
      <div class="flex items-center text-nordic-600 group-hover:text-primary-600 font-medium">
        Explore System <ArrowRight class="h-4 w-4 ml-2" />
      </div>
    </a>

  </div>

  <!-- Key Features -->
  <div class="bg-white rounded-xl shadow-lg p-8">
    <h2 class="text-2xl font-bold text-nordic-800 mb-6 text-center">
      Prototype Features
    </h2>
    
    <div class="grid md:grid-cols-3 gap-6 text-center">
      <div>
        <div class="w-12 h-12 bg-primary-100 rounded-lg flex items-center justify-center mx-auto mb-3">
          <Shield class="h-6 w-6 text-primary-600" />
        </div>
        <h4 class="font-semibold text-nordic-800 mb-2">Omni-Channel Experience</h4>
        <p class="text-nordic-600 text-sm">Seamless transitions between portal, email, SMS, and human interactions</p>
      </div>
      
      <div>
        <div class="w-12 h-12 bg-primary-100 rounded-lg flex items-center justify-center mx-auto mb-3">
          <Target class="h-6 w-6 text-primary-600" />
        </div>
        <h4 class="font-semibold text-nordic-800 mb-2">Contextual Recommendations</h4>
        <p class="text-nordic-600 text-sm">AI-driven suggestions based on company profile and behavior</p>
      </div>
      
      <div>
        <div class="w-12 h-12 bg-primary-100 rounded-lg flex items-center justify-center mx-auto mb-3">
          <Bolt class="h-6 w-6 text-primary-600" />
        </div>
        <h4 class="font-semibold text-nordic-800 mb-2">Progressive Intelligence</h4>
        <p class="text-nordic-600 text-sm">Evolution from simple rules to machine learning to AI-powered insights</p>
      </div>
    </div>
  </div>
</div>

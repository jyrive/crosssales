<script>
  let { size = 24, color = "currentColor", strokeWidth = 2, ...props } = $props();
</script>

<svg 
  width={size} 
  height={size} 
  viewBox="0 0 24 24" 
  fill="none" 
  stroke={color} 
  stroke-width={strokeWidth}
  stroke-linecap="round" 
  stroke-linejoin="round"
  {...props}
>
  <path d="M9 18l6-6l-6-6"/>
</svg>
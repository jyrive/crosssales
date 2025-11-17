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
  <polygon points="13,2 3,14 12,14 11,22 21,10 12,10"/>
</svg>
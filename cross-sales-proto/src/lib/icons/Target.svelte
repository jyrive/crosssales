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
  <path d="M12 2L2 7l10 5l10-5l-10-5Z"/>
  <path d="M2 17l10 5l10-5"/>
  <path d="M2 12l10 5l10-5"/>
</svg>
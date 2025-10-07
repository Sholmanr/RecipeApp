<script>
  const url = import.meta.env.PUBLIC_SUPABASE_URL;
  const key = import.meta.env.PUBLIC_SUPABASE_ANON_KEY;
  
  console.log('URL:', url);
  console.log('Key:', key);
</script>

<h1>Environment Variable Test</h1>
<p>URL: {url || 'UNDEFINED'}</p>
<p>Key: {key ? 'LOADED' : 'UNDEFINED'}</p>
<script lang="ts">
  import "../app.css";
  let { children } = $props();
  import AppBar from "../components/appBar.svelte";
</script>

<AppBar></AppBar>

{@render children()}

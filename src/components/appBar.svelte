<script lang="ts">
  import { AppBar } from "@skeletonlabs/skeleton-svelte";
  import ArrowLeft from "@lucide/svelte/icons/arrow-left";
  import Paperclip from "@lucide/svelte/icons/paperclip";
  import Calendar from "@lucide/svelte/icons/calendar";
  import CircleUser from "@lucide/svelte/icons/circle-user";
  import Menu from "@lucide/svelte/icons/menu";
  import LightSwitch from "./lightSwitch.svelte";

  const themes = ["cerberus", "mona", "vox", "catppuccin", "mint", "seafoam"];

  function setTheme(theme: string) {
    document.documentElement.setAttribute("data-theme", theme);
  }
</script>

<AppBar headlineClasses="sm:hidden" centerClasses="hidden sm:block">
  {#snippet trail()}
    <div class="flex items-center gap-5">
      {#each themes as theme}
        <button
          class="badge preset-filled-primary-500"
          on:click={() => setTheme(theme)}
        >
          {theme}
        </button>
      {/each}
      <LightSwitch />
    </div>
  {/snippet}
  <h1 class="h1 mb-4">SkeletonUI To-Do App</h1>
</AppBar>

<script>
  import "../app.pcss";
  import { ModeWatcher } from "mode-watcher";

  import { Button } from "$lib/components/ui/button";
  import { Sun, Moon } from "lucide-svelte";
  import { toggleMode } from "mode-watcher";
</script>

<ModeWatcher />
<div class="h-[32rem] grid grid-rows-[auto,1fr]">
  <div
    class="flex justify-between items-baseline space-x-2 p-2 border-b border-gray-200 dark:border-gray-800"
  >
  <div>

    <h1 class="text-2xl font-bold">Sondaggi Capodanno</h1>
    <p class="text-xs">Domande a caso da chatGPT</p>
  </div>
    <Button on:click={toggleMode} variant="outline" size="icon">
      <Sun
        class="h-[1.2rem] w-[1.2rem] rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0"
      />
      <Moon
        class="absolute h-[1.2rem] w-[1.2rem] rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100"
      />
      <span class="sr-only">Toggle theme</span>
    </Button>
  </div>
  

  <slot />
</div>

<script lang="ts">
	import { Accordion, AccordionItem } from "flowbite-svelte";
	import { onMount } from "svelte";



  interface Tool {
    id: string;
    description: string;
    meta_version: string;
    url: string;
  }

  const fetchTools = async (): Promise<Tool[]> => {
    const response = await fetch('https://trs-filer-test.rahtiapp.fi/ga4gh/trs/v2/tools?limit=20');
    const data = await response.json();
    return data;
  };

  let tools: Tool[] = [];

  onMount(async () => {
    tools = await fetchTools();
  });


</script>

<div class="container mx-auto mt-10">
  <p class="text-4xl dark:text-white mb-5">TRS component</p>
  <p class="text-lg dark:text-white mb-5">Rendered using SvelteKit, Tailwind CSS and Flowbite-Svelte</p>
  {#if tools.length}
  <Accordion 
      activeClasses="bg-blue-100 dark:bg-gray-800 text-blue-600 dark:text-white focus:ring-4 focus:ring-blue-200 dark:focus:ring-blue-800" 
      inactiveClasses="text-gray-500 dark:text-gray-400 hover:bg-blue-100 dark:hover:bg-gray-800">
    {#each tools as item}
      <AccordionItem class="">
      <span slot="header">{`Tool with id: ${item.id}`}</span>
      <a href={item.url}>url: <span class="underline text-blue-800 hover:no-underline">{item.url}</span></a>
      <p class="text-gray-500 dark:text-gray-400">{`description: ${item.description}`}</p>
      <p class="mb-2 text-gray-500 dark:text-gray-400">{`version: ${item.meta_version}`}</p>
      </AccordionItem>
    {/each}
  </Accordion>
  {:else}
    <p>Loading...</p>
  {/if}
</div>

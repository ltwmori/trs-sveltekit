<script context="module" lang="ts">
	export interface AccordionProps {
	  items: { header: string; content: string }[];
	//   activeClasses: string;
	//   inactiveClasses: string;
	}
	export let props: AccordionProps;
  </script>
  
  <script lang="ts">
	import { AccordionItem, Accordion } from 'flowbite-svelte';
  </script>
  <!-- activeClasses={props.activeClasses} inactiveClasses={props.inactiveClasses} -->
  <Accordion 
  	activeClasses="bg-blue-100 dark:bg-gray-800 text-blue-600 dark:text-white focus:ring-4 focus:ring-blue-200 dark:focus:ring-blue-800" 
  	inactiveClasses="text-gray-500 dark:text-gray-400 hover:bg-blue-100 dark:hover:bg-gray-800">
	{#each props.items as item}
	  <AccordionItem class="">
		<span slot="header">{item.header}</span>
		<p class="mb-2 text-gray-500 dark:text-gray-400">{item.content}</p>
	  </AccordionItem>
	{/each}
  </Accordion>
  
<script>
  import Loading from "../components/Loading.svelte";
import Main from "../components/Main.svelte";
  import Panel from "../components/Panel.svelte";
  export let users;
  import { onMount } from 'svelte';

  let loading = true;

 onMount(() => {
  setTimeout(() => {
    loading = false;
  }, 150);
});
</script>

<div>
  {#if loading}
  <div class="flex justify-center min-h-screen items-center">
    <div
      class="mb-1.5 w-full max-w-sm p-4 bg-white border border-gray-200 rounded-lg shadow sm:p-6 md:p-8 dark:bg-gray-800 dark:border-gray-700"
    >
<Loading />
<h3 class="text-2xl font-semibold whitespace-nowrap dark:text-white text-center">Loading</h3>
</div>
</div>
  {:else if users}
    <Panel {users} />
  {:else}
    <Main />
  {/if}
</div>

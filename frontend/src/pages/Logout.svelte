<script>
  import { onMount } from 'svelte';
  import Loading from '../components/Loading.svelte';
  import Cookies from "js-cookie";
let loading = true;

onMount(() => {
setTimeout(() => {
  loading = false;
  Cookies.remove('token')
  window.location.href = "/";
}, 4000);
});
</script>

<main>
    {#if loading}
    <div class="flex justify-center min-h-screen items-center">
        <div
          class="mb-1.5 w-full max-w-sm p-4 bg-white border border-gray-200 rounded-lg shadow sm:p-6 md:p-8 dark:bg-gray-800 dark:border-gray-700"
        >
    <Loading />
    <h3 class="text-2xl font-semibold whitespace-nowrap dark:text-white text-center">Çıkış Yapılıyor</h3>
    </div>
</div>
    {/if}
</main>
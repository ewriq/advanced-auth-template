
<script>
    // @ts-ignore
    import Cookies from "js-cookie";
    import axios from "axios";
  
    let email = "";
    let password = "";
    let error = "";
    let username = "";
  
    async function register() {
      const form = {
        email: email,
        password: password,
        username: username,
      };
  
      try {
        const response = await axios.post(
          "http://localhost:3000/api/auth/register",
          form
        );
        console.log("saa", response.data);
        if (response.data.status === "OK") {
          const data = response.data;
          const token = data.token;
          Cookies.set("token", token);
          // @ts-ignore
          error = "Başarılı işlem birazdan yönlendiriliyorsunuz !";
          setTimeout(function () {
            window.location.href = "/";
          }, 3000);
        } else {
          error = "Bir hata oluştu.";
          console.error("Bir hata oluştu.");
        }
      } catch (error) {
        console.error("İstek gönderilirken hata oluştu:", error);
      }
    }
  </script>
  
  <main>
  
    <div class="flex justify-center min-h-screen items-center">
        <div
          class="mb-1.5 w-full max-w-sm p-4 bg-white border border-gray-200 rounded-lg shadow sm:p-6 md:p-8 dark:bg-gray-800 dark:border-gray-700"
        >
          <form class="space-y-6" action="#">
            <h5 class="text-xl font-medium text-gray-900 dark:text-white">Register</h5>
            {#if error}
              <div class="bg-green-100 text-green-700 p-4" role="alert">
                <p class="font-bold">{error}</p>
              </div>
            {/if}
            <div>
                <label
                  for="username"
                  class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                  >Your username</label
                >
                <input
                  type="username"
                  bind:value={username}
                  id="username"
                  class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white"
                  placeholder="company"
                  required
                />
              </div>
            <div>
              <label
                for="email"
                class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                >Your email</label
              >
              <input
                type="email"
                bind:value={email}
                id="email"
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white"
                placeholder="name@company.com"
                required
              />
            </div>
            <div>
              <label
                for="password"
                class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                >Your password</label
              >
              <input
                type="password"
                bind:value={password}
                id="password"
                placeholder="••••••••"
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white"
                required
              />
            </div>
    
            <button
              on:click|preventDefault={register}
              type="submit"
              class="w-full text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
              >Register</button
            >
          </form>
        </div>
      </div>
  </main>
  
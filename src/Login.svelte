<script>
  // Svelte component logic
  let email = "";
  let password = "";
  let showPassword = false;

  function handleSubmit() {
    console.log("Login submitted:", { email, password });

    localStorage.setItem("userEmail", email);
    localStorage.setItem("userPassword", password);
  }

  function togglePasswordVisibility() {
    showPassword = !showPassword;
  }
</script>

<div
  class="flex items-center justify-center min-h-[calc(100vh-10px)] w-[calc(100vw-10px)] bg-[#f2f4f8]"
>
  <div
    class="min-h-[70vh] max-w-7xl flex sm:w-[90%] md:w-[80%] lg:w-[70%] mx-auto rounded-lg overflow-hidden shadow-lg"
  >
    <!-- Left side - Blue section with logo and text -->
    <div class="flex-1 bg-[#4990c0] text-white p-8 flex flex-col">
      <div class="mb-12 mt-8">
        <div class="inline-block bg-white text-black py-2 px-4 rounded-lg">
          <div class="flex items-center">
            <svg
              class="w-6 h-6 mr-2"
              viewBox="0 0 24 24"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path d="M12 2L2 7L12 12L22 7L12 2Z" fill="currentColor" />
              <path
                d="M2 17L12 22L22 17"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
              <path
                d="M2 12L12 17L22 12"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </svg>
            <span class="font-bold">TRACKIER demo</span>
          </div>
        </div>
      </div>

      <div class="grow flex flex-col justify-center">
        <h1 class="text-3xl font-bold mb-4">
          Access your TRACKIER demo Dashboard
        </h1>
        <p class="text-lg">
          Log in to manage your partnerships and track your earnings
          effortlessly.
        </p>
      </div>

      <!-- Dashboard preview image -->
      <div class="mt-8 mb-4">
        <div class="bg-white rounded-lg p-2 shadow-md">
          <div class="flex items-center bg-gray-100 mb-2">
            <div class="flex space-x-1 ml-2">
              <div class="w-3 h-3 bg-red-500 rounded-full"></div>
              <div class="w-3 h-3 bg-yellow-500 rounded-full"></div>
              <div class="w-3 h-3 bg-green-500 rounded-full"></div>
            </div>
            <div class="flex-grow text-center">
              <div class="w-24 h-4 bg-gray-300 mx-auto my-1 rounded"></div>
            </div>
            <div class="mr-2">×</div>
          </div>

          <div class="flex">
            <!-- Left sidebar in the preview -->
            <div
              class="w-12 bg-[#1a1a47] h-48 flex flex-col items-center py-2 space-y-4"
            >
              <div class="w-6 h-6 bg-gray-300 rounded"></div>
              <div class="w-6 h-6 bg-gray-300 rounded-full"></div>
              <div class="w-6 h-6 bg-gray-300 rounded-full"></div>
              <div class="w-6 h-6 bg-gray-300 rounded-full"></div>
              <div class="w-6 h-6 bg-gray-300 rounded-full"></div>
            </div>

            <!-- Main content area in the preview -->
            <div class="flex-grow p-2">
              <div class="w-full h-10 bg-gray-200 rounded mb-4"></div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Right side - Login form -->
    <div class="flex-1 bg-white p-8 flex flex-col justify-center">
      <div class="max-w-md w-full mx-auto">
        <h2 class="text-2xl font-semibold mb-8">Login</h2>

        <form on:submit|preventDefault={handleSubmit}>
          <div class="mb-4">
            <label
              for="email"
              class="block text-sm font-medium text-gray-700 mb-1"
            >
              Email <span class="text-red-500">*</span>
            </label>
            <div class="relative">
              <div
                class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none"
              >
                <svg
                  class="h-5 w-5 text-gray-400"
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 20 20"
                  fill="currentColor"
                >
                  <path
                    d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z"
                  />
                </svg>
              </div>
              <input
                type="email"
                id="email"
                bind:value={email}
                required
                class="pl-10 block w-full rounded-md border-gray-300 shadow-sm py-2 px-3 border focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                placeholder="Email"
              />
            </div>
          </div>

          <div class="mb-4">
            <label
              for="password"
              class="block text-sm font-medium text-gray-700 mb-1"
            >
              Password <span class="text-red-500">*</span>
            </label>
            <div class="relative">
              {#if showPassword}
                <input
                  type="text"
                  id="password"
                  bind:value={password}
                  required
                  class="block w-full rounded-md border-gray-300 shadow-sm py-2 px-3 border focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                  placeholder="Password"
                />
              {:else}
                <input
                  type="password"
                  id="password"
                  bind:value={password}
                  required
                  class="block w-full rounded-md border-gray-300 shadow-sm py-2 px-3 border focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                  placeholder="Password"
                />
              {/if}
              <button
                type="button"
                class="absolute inset-y-0 right-0 flex items-center px-3"
                on:click={togglePasswordVisibility}
              >
                {#if showPassword}
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    class="h-5 w-5 text-gray-400"
                    viewBox="0 0 20 20"
                    fill="currentColor"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M3.707 2.293a1 1 0 00-1.414 1.414l14 14a1 1 0 001.414-1.414l-1.473-1.473A10.014 10.014 0 0019.542 10C18.268 5.943 14.478 3 10 3a9.958 9.958 0 00-4.512 1.074l-1.78-1.781zm4.261 4.26l1.514 1.515a2.003 2.003 0 012.45 2.45l1.514 1.514a4 4 0 00-5.478-5.478z"
                      clip-rule="evenodd"
                    />
                    <path
                      d="M12.454 16.697L9.75 13.992a4 4 0 01-3.742-3.741L2.335 6.578A9.98 9.98 0 00.458 10c1.274 4.057 5.065 7 9.542 7 .847 0 1.669-.105 2.454-.303z"
                    />
                  </svg>
                {:else}
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    class="h-5 w-5 text-gray-400"
                    viewBox="0 0 20 20"
                    fill="currentColor"
                  >
                    <path d="M10 12a2 2 0 100-4 2 2 0 000 4z" />
                    <path
                      fill-rule="evenodd"
                      d="M.458 10C1.732 5.943 5.522 3 10 3s8.268 2.943 9.542 7c-1.274 4.057-5.064 7-9.542 7S1.732 14.057.458 10zM14 10a4 4 0 11-8 0 4 4 0 018 0z"
                      clip-rule="evenodd"
                    />
                  </svg>
                {/if}
              </button>
            </div>
          </div>

          <div class="mb-6 text-sm">
            <a
              href="#forgot-password"
              class="text-blue-500 hover:text-blue-700 flex items-center"
            >
              <svg
                class="w-4 h-4 mr-1"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"
                />
              </svg>
              Forgot your password?
            </a>
          </div>

          <button
            type="submit"
            class="w-full bg-blue-500 hover:bg-blue-600 text-white font-medium py-2 px-4 rounded-md transition-colors"
          >
            Log In
          </button>
        </form>

        <div class="mt-8">
          <div class="flex items-center justify-center">
            <div class="border-t border-gray-300 flex-grow"></div>
            <div class="mx-4 text-sm text-gray-500">or</div>
            <div class="border-t border-gray-300 flex-grow"></div>
          </div>

          <button
            class="mt-6 w-full flex justify-center items-center bg-white border border-gray-300 rounded-md shadow-sm py-2 px-4 text-sm font-medium text-gray-700 hover:bg-gray-50"
          >
            <svg
              class="w-5 h-5 mr-2"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 24 24"
            >
              <path
                d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"
                fill="#4285F4"
              />
              <path
                d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"
                fill="#34A853"
              />
              <path
                d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z"
                fill="#FBBC05"
              />
              <path
                d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z"
                fill="#EA4335"
              />
            </svg>
            Sign in with Google
          </button>
        </div>

        <div class="mt-8 text-center">
          <p class="text-sm text-gray-600">Don't have an account?</p>
          <div class="mt-3">
            <a href="/#/signup" class="text-blue-500 hover:text-blue-700 font-medium">
              Sign up
            </a>
          </div>
        </div>

        <div class="mt-6 text-xs text-center text-gray-600">
          <p>
            You must have <a href="#cookies" class="text-blue-500"
              >cookies enabled</a
            > to use this site (cookies enabled)
          </p>
          <a href="#terms" class="text-blue-500">terms and conditions</a>
        </div>
      </div>
    </div>
  </div>
</div>

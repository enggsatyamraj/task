<script>
  import { onMount } from "svelte";

  // State for metrics data
  let clicks = { today: 16, yesterday: 18, mtd: 81 };
  let conversions = { today: 0, yesterday: 0, mtd: 2 };
  let impressions = { today: 0, yesterday: 0, mtd: 0 };

  // State for data from JSONPlaceholder API
  let posts = [];
  let isLoading = true;
  let error = null;

  // Sidebar state
  let isSidebarCollapsed = false;
  let isMobileSidebarOpen = false;

  // Current date range
  let dateRange = "2025-05-08 - 2025-05-14";

  function toggleSidebar() {
    isSidebarCollapsed = !isSidebarCollapsed;
  }

  function toggleMobileSidebar() {
    isMobileSidebarOpen = !isMobileSidebarOpen;
  }

  // Dummy function for action buttons
  function handleAction() {
    alert("Action clicked");
  }

  function customizeWidgets() {
    alert("Customize widgets clicked");
  }

  // Fetch data from JSONPlaceholder API
  onMount(async () => {
    try {
      // Auto-collapse sidebar on small screens
      if (window.innerWidth < 768) {
        isSidebarCollapsed = true;
      }

      // Add event listener for window resize
      window.addEventListener("resize", () => {
        if (window.innerWidth < 768) {
          isSidebarCollapsed = true;
        }
      });

      // Fetch posts
      const postsResponse = await fetch(
        "https://jsonplaceholder.typicode.com/posts?_limit=10"
      );
      if (!postsResponse.ok) {
        throw new Error(`HTTP error! Status: ${postsResponse.status}`);
      }
      posts = await postsResponse.json();
      isLoading = false;
    } catch (err) {
      console.error("Error fetching data:", err);
      error = err.message;
      isLoading = false;
    }

    return () => {
      // Clean up event listeners
      window.removeEventListener("resize");
    };
  });
</script>

<div class="flex flex-col lg:flex-row h-screen bg-gray-100 overflow-hidden">
  <!-- Mobile Sidebar Overlay -->
  {#if isMobileSidebarOpen}
    <div
      class="fixed inset-0 bg-gray-600 bg-opacity-75 z-20 lg:hidden"
      on:click={toggleMobileSidebar}
    ></div>
  {/if}

  <!-- Sidebar -->
  <div
    class={`
        fixed inset-y-0 left-0 z-30 transform lg:relative lg:transform-none transition duration-300 ease-in-out
        bg-[#3B83BD] text-white 
        ${isMobileSidebarOpen ? "translate-x-0" : "-translate-x-full lg:translate-x-0"} 
        ${isSidebarCollapsed ? "w-20 lg:w-16" : "w-72 lg:w-64"}
      `}
  >
    <!-- Logo -->
    <div class="flex items-center px-4 py-5">
      <div class="flex-shrink-0">
        <svg
          class="w-8 h-8 text-white"
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
      </div>
      {#if !isSidebarCollapsed}
        <div class="ml-3 text-xl font-bold">TRACKIER</div>
      {/if}
    </div>

    <!-- Login/Signup buttons visible in mobile sidebar -->
    {#if !isSidebarCollapsed && isMobileSidebarOpen}
      <div
        class="px-4 py-3 border-t border-b border-blue-700 mb-2 flex flex-col space-y-2 lg:hidden"
      >
        <a
          href="/#/login"
          class="flex items-center px-2 py-2 bg-white text-blue-700 rounded-md hover:bg-gray-100 transition"
        >
          <svg
            class="w-5 h-5 mr-2"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M11 16l-4-4m0 0l4-4m-4 4h14m-5 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h7a3 3 0 013 3v1"
            ></path>
          </svg>
          <span class="font-medium">Login</span>
        </a>
        <a
          href="/#/signup"
          class="flex items-center px-2 py-2 bg-white text-blue-700 rounded-md hover:bg-gray-100 transition"
        >
          <svg
            class="w-5 h-5 mr-2"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M18 9v3m0 0v3m0-3h3m-3 0h-3m-2-5a4 4 0 11-8 0 4 4 0 018 0zM3 20a6 6 0 0112 0v1H3v-1z"
            ></path>
          </svg>
          <span class="font-medium text-white">Signup</span>
        </a>
      </div>
    {/if}

    <!-- Navigation -->
    <nav class="mt-5 px-2 overflow-y-auto h-[calc(100vh-10rem)]">
      <div>
        <a
          href="/"
          class="flex items-center px-2 py-3 text-white hover:bg-blue-700 rounded-md"
        >
          <svg
            class="w-5 h-5"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"
            ></path>
          </svg>
          {#if !isSidebarCollapsed}
            <span class="ml-3">Dashboard</span>
          {/if}
        </a>

        <a
          href="#campaigns"
          class="flex items-center px-2 py-3 text-white hover:bg-blue-700 rounded-md group"
        >
          <svg
            class="w-5 h-5"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"
            ></path>
          </svg>
          {#if !isSidebarCollapsed}
            <span class="ml-3">Campaigns</span>
            <svg
              class="ml-auto w-4 h-4"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M9 5l7 7-7 7"
              ></path>
            </svg>
          {/if}
        </a>

        <a
          href="#reports"
          class="flex items-center px-2 py-3 text-white hover:bg-blue-700 rounded-md group"
        >
          <svg
            class="w-5 h-5"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"
            ></path>
          </svg>
          {#if !isSidebarCollapsed}
            <span class="ml-3">Reports</span>
            <svg
              class="ml-auto w-4 h-4"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M9 5l7 7-7 7"
              ></path>
            </svg>
          {/if}
        </a>

        <a
          href="#publishers"
          class="flex items-center px-2 py-3 text-white hover:bg-blue-700 rounded-md group"
        >
          <svg
            class="w-5 h-5"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"
            ></path>
          </svg>
          {#if !isSidebarCollapsed}
            <span class="ml-3">Publishers</span>
            <svg
              class="ml-auto w-4 h-4"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M9 5l7 7-7 7"
              ></path>
            </svg>
          {/if}
        </a>

        <a
          href="#advertisers"
          class="flex items-center px-2 py-3 text-white hover:bg-blue-700 rounded-md group"
        >
          <svg
            class="w-5 h-5"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4"
            ></path>
          </svg>
          {#if !isSidebarCollapsed}
            <span class="ml-3">Advertisers</span>
            <svg
              class="ml-auto w-4 h-4"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M9 5l7 7-7 7"
              ></path>
            </svg>
          {/if}
        </a>

        <a
          href="#invoices"
          class="flex items-center px-2 py-3 text-white hover:bg-blue-700 rounded-md group"
        >
          <svg
            class="w-5 h-5"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-3 7h3m-3 4h3m-6-4h.01M9 16h.01"
            ></path>
          </svg>
          {#if !isSidebarCollapsed}
            <span class="ml-3">Invoices</span>
            <svg
              class="ml-auto w-4 h-4"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M9 5l7 7-7 7"
              ></path>
            </svg>
          {/if}
        </a>

        <a
          href="#automation"
          class="flex items-center px-2 py-3 text-white hover:bg-blue-700 rounded-md group"
        >
          <svg
            class="w-5 h-5"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z"
            ></path>
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"
            ></path>
          </svg>
          {#if !isSidebarCollapsed}
            <span class="ml-3">Automation</span>
            <svg
              class="ml-auto w-4 h-4"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M9 5l7 7-7 7"
              ></path>
            </svg>
          {/if}
        </a>

        <a
          href="#customize"
          class="flex items-center px-2 py-3 text-white hover:bg-blue-700 rounded-md"
        >
          <svg
            class="w-5 h-5"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M11 4a2 2 0 114 0v1a1 1 0 001 1h3a1 1 0 011 1v3a1 1 0 01-1 1h-1a2 2 0 100 4h1a1 1 0 011 1v3a1 1 0 01-1 1h-3a1 1 0 01-1-1v-1a2 2 0 10-4 0v1a1 1 0 01-1 1H7a1 1 0 01-1-1v-3a1 1 0 00-1-1H4a2 2 0 110-4h1a1 1 0 001-1V7a1 1 0 011-1h3a1 1 0 001-1V4z"
            ></path>
          </svg>
          {#if !isSidebarCollapsed}
            <span class="ml-3">Customize</span>
          {/if}
        </a>

        <a
          href="#notification"
          class="flex items-center px-2 py-3 text-white hover:bg-blue-700 rounded-md"
        >
          <svg
            class="w-5 h-5"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"
            ></path>
          </svg>
          {#if !isSidebarCollapsed}
            <span class="ml-3">Notification</span>
          {/if}
        </a>

        <a
          href="#support"
          class="flex items-center px-2 py-3 text-white hover:bg-blue-700 rounded-md"
        >
          <svg
            class="w-5 h-5"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M18.364 5.636l-3.536 3.536m0 5.656l3.536 3.536M9.172 9.172L5.636 5.636m3.536 9.192l-3.536 3.536M21 12a9 9 0 11-18 0 9 9 0 0118 0zm-5 0a4 4 0 11-8 0 4 4 0 018 0z"
            ></path>
          </svg>
          {#if !isSidebarCollapsed}
            <span class="ml-3">Support</span>
          {/if}
        </a>

        <a
          href="#billing"
          class="flex items-center px-2 py-3 text-white hover:bg-blue-700 rounded-md"
        >
          <svg
            class="w-5 h-5"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z"
            ></path>
          </svg>
          {#if !isSidebarCollapsed}
            <span class="ml-3">Billing</span>
          {/if}
        </a>
      </div>
    </nav>

    <!-- Collapse Button -->
    <div
      class="mt-auto border-t border-blue-700 pt-2 pb-3 px-4 hidden lg:block"
    >
      <button
        on:click={toggleSidebar}
        class="flex items-center px-2 py-2 text-white hover:bg-blue-700 rounded-md w-full"
      >
        <svg
          class="w-5 h-5"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
          xmlns="http://www.w3.org/2000/svg"
        >
          {#if isSidebarCollapsed}
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M13 5l7 7-7 7M5 5l7 7-7 7"
            ></path>
          {:else}
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M11 19l-7-7 7-7m8 14l-7-7 7-7"
            ></path>
          {/if}
        </svg>
        {#if !isSidebarCollapsed}
          <span class="ml-3">Collapse</span>
        {/if}
      </button>
    </div>
  </div>

  <!-- Main Content -->
  <div class="flex-1 flex flex-col overflow-hidden w-full">
    <!-- Top Header -->
    <header class="bg-white shadow-sm">
      <div class="flex justify-between items-center px-4 sm:px-6 py-3">
        <div class="flex items-center">
          <!-- Mobile menu button -->
          <button
            class="inline-flex items-center justify-center p-2 rounded-md text-gray-600 hover:text-gray-900 hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-blue-500 lg:hidden"
            on:click={toggleMobileSidebar}
          >
            <svg
              class="w-6 h-6"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M4 6h16M4 12h16M4 18h16"
              ></path>
            </svg>
          </button>
          <h1 class="text-xl font-semibold text-gray-800 ml-2 lg:ml-0">
            Dashboard
          </h1>
        </div>
        <div class="flex items-center space-x-2 sm:space-x-4">
          <!-- Login and Signup buttons - Always visible in the header -->
          <div class="flex space-x-1 sm:space-x-4">
            <a
              href="/#/login"
              class="bg-blue-50 text-blue-700 px-2 sm:px-3 py-1.5 sm:py-2 rounded-md text-sm font-medium border border-blue-200 hover:bg-blue-100 transition"
            >
              Login
            </a>
            <a
              href="/#/signup"
              class="bg-blue-600 text-white px-2 sm:px-3 py-1.5 sm:py-2 rounded-md text-sm font-medium hover:bg-blue-700 transition"
            >
              Signup
            </a>
          </div>

          <!-- Actions Dropdown - Hidden on small screens -->
          <div class="relative hidden sm:block">
            <button
              class="flex items-center px-3 py-2 bg-gray-200 text-gray-700 rounded-md hover:bg-gray-300 transition"
            >
              Actions
              <svg
                class="ml-1 w-4 h-4"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M19 9l-7 7-7-7"
                ></path>
              </svg>
            </button>
          </div>

          <!-- Notifications -->
          <div class="relative">
            <button class="text-gray-500 hover:text-gray-700">
              <span
                class="absolute -top-1 -right-1 bg-red-500 text-white text-xs rounded-full h-4 w-4 flex items-center justify-center"
              >
                1
              </span>
              <svg
                class="w-6 h-6"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"
                ></path>
              </svg>
            </button>
          </div>

          <!-- Profile -->
          <div>
            <button
              class="h-8 w-8 rounded-full overflow-hidden border-2 border-gray-300"
            >
              <img
                src="https://via.placeholder.com/40"
                alt="Profile"
                class="h-full w-full object-cover"
              />
            </button>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content Area -->
    <main class="flex-1 overflow-y-auto bg-gray-100 p-4 sm:p-6">
      <!-- Performance Report Section -->
      <div class="bg-white shadow rounded-lg mb-6 p-4">
        <div
          class="flex flex-col sm:flex-row justify-between items-start sm:items-center mb-4 space-y-3 sm:space-y-0"
        >
          <h2 class="text-lg font-medium text-gray-800">PERFORMANCE REPORT</h2>
          <div class="w-full sm:w-auto">
            <div class="relative">
              <input
                type="text"
                value={dateRange}
                class="block w-full px-4 py-2 text-gray-700 bg-white border border-gray-300 rounded-md focus:outline-none"
                readonly
              />
              <div
                class="absolute inset-y-0 right-0 flex items-center px-2 pointer-events-none"
              >
                <svg
                  class="w-5 h-5 text-gray-500"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"
                  ></path>
                </svg>
              </div>
            </div>
          </div>
        </div>

        <!-- Performance Content Here (Placeholder) -->
        <div
          class="h-48 sm:h-64 flex items-center justify-center border border-gray-200 rounded-lg bg-gray-50"
        >
          <p class="text-gray-500">Performance graph would appear here</p>
        </div>
      </div>

      <!-- Metrics Cards -->
      <div
        class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 sm:gap-6 mb-6"
      >
        <!-- Clicks -->
        <div class="bg-white shadow rounded-lg overflow-hidden">
          <div class="p-4 border-b border-gray-200">
            <div class="flex items-center">
              <div class="flex-shrink-0 bg-gray-100 rounded-full p-3">
                <svg
                  class="w-5 h-5 sm:w-6 sm:h-6 text-gray-500"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M15 15l-2 5L9 9l11 4-5 2zm0 0l5 5M7.188 2.239l.777 2.897M5.136 7.965l-2.898-.777M13.95 4.05l-2.122 2.122m-5.657 5.656l-2.12 2.122"
                  ></path>
                </svg>
              </div>
              <h3 class="ml-3 text-base sm:text-lg font-medium text-gray-900">
                CLICKS
              </h3>
            </div>
          </div>
          <div class="grid grid-cols-3 divide-x divide-gray-200">
            <div class="p-3 sm:p-4 text-center">
              <p class="text-xs sm:text-sm font-medium text-gray-500">Today</p>
              <p class="mt-1 text-xl sm:text-3xl font-semibold text-blue-600">
                {clicks.today}
              </p>
            </div>
            <div class="p-3 sm:p-4 text-center">
              <p class="text-xs sm:text-sm font-medium text-gray-500">
                Yesterday
              </p>
              <p class="mt-1 text-xl sm:text-3xl font-semibold text-blue-600">
                {clicks.yesterday}
              </p>
            </div>
            <div class="p-3 sm:p-4 text-center">
              <p class="text-xs sm:text-sm font-medium text-gray-500">MTD</p>
              <p class="mt-1 text-xl sm:text-3xl font-semibold text-blue-600">
                {clicks.mtd}
              </p>
            </div>
          </div>
        </div>

        <!-- Conversions -->
        <div class="bg-white shadow rounded-lg overflow-hidden">
          <div class="p-4 border-b border-gray-200">
            <div class="flex items-center">
              <div class="flex-shrink-0 bg-gray-100 rounded-full p-3">
                <svg
                  class="w-5 h-5 sm:w-6 sm:h-6 text-gray-500"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"
                  ></path>
                </svg>
              </div>
              <h3 class="ml-3 text-base sm:text-lg font-medium text-gray-900">
                CONVERSIONS
              </h3>
            </div>
          </div>
          <div class="grid grid-cols-3 divide-x divide-gray-200">
            <div class="p-3 sm:p-4 text-center">
              <p class="text-xs sm:text-sm font-medium text-gray-500">Today</p>
              <p class="mt-1 text-xl sm:text-3xl font-semibold text-blue-600">
                {conversions.today}
              </p>
            </div>
            <div class="p-3 sm:p-4 text-center">
              <p class="text-xs sm:text-sm font-medium text-gray-500">
                Yesterday
              </p>
              <p class="mt-1 text-xl sm:text-3xl font-semibold text-blue-600">
                {conversions.yesterday}
              </p>
            </div>
            <div class="p-3 sm:p-4 text-center">
              <p class="text-xs sm:text-sm font-medium text-gray-500">MTD</p>
              <p class="mt-1 text-xl sm:text-3xl font-semibold text-blue-600">
                {conversions.mtd}
              </p>
            </div>
          </div>
        </div>

        <!-- Impressions -->
        <div
          class="bg-white shadow rounded-lg overflow-hidden sm:col-span-2 lg:col-span-1"
        >
          <div class="p-4 border-b border-gray-200">
            <div class="flex items-center">
              <div class="flex-shrink-0 bg-gray-100 rounded-full p-3">
                <svg
                  class="w-5 h-5 sm:w-6 sm:h-6 text-gray-500"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"
                  ></path>
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"
                  ></path>
                </svg>
              </div>
              <h3 class="ml-3 text-base sm:text-lg font-medium text-gray-900">
                IMPRESSIONS
              </h3>
            </div>
          </div>
          <div class="grid grid-cols-3 divide-x divide-gray-200">
            <div class="p-3 sm:p-4 text-center">
              <p class="text-xs sm:text-sm font-medium text-gray-500">Today</p>
              <p class="mt-1 text-xl sm:text-3xl font-semibold text-blue-600">
                {impressions.today}
              </p>
            </div>
            <div class="p-3 sm:p-4 text-center">
              <p class="text-xs sm:text-sm font-medium text-gray-500">
                Yesterday
              </p>
              <p class="mt-1 text-xl sm:text-3xl font-semibold text-blue-600">
                {impressions.yesterday}
              </p>
            </div>
            <div class="p-3 sm:p-4 text-center">
              <p class="text-xs sm:text-sm font-medium text-gray-500">MTD</p>
              <p class="mt-1 text-xl sm:text-3xl font-semibold text-blue-600">
                {impressions.mtd}
              </p>
            </div>
          </div>
        </div>
      </div>

      <!-- Customize Widgets Button -->
      <div class="flex justify-center mb-6">
        <button
          on:click={customizeWidgets}
          class="flex items-center px-3 py-2 sm:px-4 sm:py-2 bg-blue-500 text-white rounded-md hover:bg-blue-600 transition text-sm sm:text-base"
        >
          <svg
            class="w-4 h-4 sm:w-5 sm:h-5 mr-1 sm:mr-2"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M11 4a2 2 0 114 0v1a1 1 0 001 1h3a1 1 0 011 1v3a1 1 0 01-1 1h-1a2 2 0 100 4h1a1 1 0 011 1v3a1 1 0 01-1 1h-3a1 1 0 01-1-1v-1a2 2 0 10-4 0v1a1 1 0 01-1 1H7a1 1 0 01-1-1v-3a1 1 0 00-1-1H4a2 2 0 110-4h1a1 1 0 001-1V7a1 1 0 011-1h3a1 1 0 001-1V4z"
            ></path>
          </svg>
          Customize Widgets
        </button>
      </div>

      <!-- JsonPlaceholder API Data -->
      <div class="bg-white shadow rounded-lg mb-6">
        <div class="p-4 border-b border-gray-200">
          <h2 class="text-base sm:text-lg font-medium text-gray-800">
            JSONPlaceholder API Data
          </h2>
        </div>

        <!-- Loading State -->
        {#if isLoading}
          <div class="p-8 flex justify-center">
            <div
              class="inline-block h-6 w-6 sm:h-8 sm:w-8 animate-spin rounded-full border-4 border-solid border-blue-500 border-r-transparent align-[-0.125em]"
            ></div>
            <span class="ml-3 text-sm sm:text-base text-gray-600"
              >Loading data...</span
            >
          </div>
        {/if}

        <!-- Error State -->
        {#if error}
          <div class="p-6 sm:p-8 text-center">
            <div
              class="inline-flex items-center justify-center w-10 h-10 sm:w-12 sm:h-12 rounded-full bg-red-100 text-red-500 mb-4"
            >
              <svg
                class="w-5 h-5 sm:w-6 sm:h-6"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
                ></path>
              </svg>
            </div>
            <p class="text-red-500 font-medium">Error loading data</p>
            <p class="mt-1 text-sm text-gray-500">{error}</p>
            <button
              class="mt-4 inline-flex items-center px-3 py-1.5 sm:px-4 sm:py-2 border border-transparent text-sm font-medium rounded-md text-blue-700 bg-blue-100 hover:bg-blue-200"
              on:click={() => window.location.reload()}
            >
              Try Again
            </button>
          </div>
        {/if}

        <!-- Data Display -->
        {#if posts.length > 0 && !isLoading && !error}
          <div class="overflow-x-auto">
            <div class="inline-block min-w-full align-middle">
              <div
                class="overflow-hidden border-b border-gray-200 sm:rounded-lg"
              >
                <table class="min-w-full divide-y divide-gray-200">
                  <thead class="bg-gray-50">
                    <tr>
                      <th
                        scope="col"
                        class="px-4 sm:px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                        >ID</th
                      >
                      <th
                        scope="col"
                        class="px-4 sm:px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                        >Title</th
                      >
                      <th
                        scope="col"
                        class="hidden sm:table-cell px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                        >Body</th
                      >
                    </tr>
                  </thead>
                  <tbody class="bg-white divide-y divide-gray-200">
                    {#each posts as post}
                      <tr>
                        <td
                          class="px-4 sm:px-6 py-3 whitespace-nowrap text-xs sm:text-sm font-medium text-gray-900"
                          >{post.id}</td
                        >
                        <td
                          class="px-4 sm:px-6 py-3 text-xs sm:text-sm text-gray-500"
                          >{post.title}</td
                        >
                        <td
                          class="hidden sm:table-cell px-6 py-3 text-xs sm:text-sm text-gray-500 truncate max-w-xs"
                          >{post.body}</td
                        >
                      </tr>
                    {/each}
                  </tbody>
                </table>
              </div>
            </div>
          </div>

          <!-- Mobile view for post details -->
          <div class="block sm:hidden p-4">
            <h3 class="text-sm font-medium text-gray-700 mb-2">
              Post Details (Mobile View)
            </h3>
            {#each posts as post}
              <div class="bg-gray-50 p-3 rounded mb-3">
                <div class="flex justify-between">
                  <span class="font-medium text-gray-700">ID: {post.id}</span>
                </div>
                <div class="mt-1">
                  <p class="text-xs font-medium">Title:</p>
                  <p class="text-xs text-gray-600">{post.title}</p>
                </div>
                <div class="mt-2">
                  <p class="text-xs font-medium">Body:</p>
                  <p class="text-xs text-gray-600 line-clamp-2">{post.body}</p>
                </div>
              </div>
            {/each}
          </div>
        {/if}

        <!-- Empty State -->
        {#if posts.length === 0 && !isLoading && !error}
          <div class="p-6 sm:p-8 text-center">
            <div
              class="inline-flex items-center justify-center w-10 h-10 sm:w-12 sm:h-12 rounded-full bg-gray-100 text-gray-500 mb-4"
            >
              <svg
                class="w-5 h-5 sm:w-6 sm:h-6"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M20 13V6a2 2 0 00-2-2H6a2 2 0 00-2 2v7m16 0v5a2 2 0 01-2 2H6a2 2 0 01-2-2v-5m16 0h-2.586a1 1 0 00-.707.293l-2.414 2.414a1 1 0 01-.707.293h-3.172a1 1 0 01-.707-.293l-2.414-2.414A1 1 0 006.586 13H4"
                ></path>
              </svg>
            </div>
            <p class="text-gray-500 font-medium">No posts found</p>
            <p class="mt-1 text-xs sm:text-sm text-gray-500">
              There are no posts available right now.
            </p>
          </div>
        {/if}
      </div>
    </main>
  </div>

  <!-- Chat Support Button (Fixed) -->
  <div class="fixed bottom-4 right-4 sm:bottom-6 sm:right-6">
    <button
      class="bg-blue-600 text-white rounded-full w-12 h-12 sm:w-14 sm:h-14 flex items-center justify-center shadow-lg hover:bg-blue-700 transition-colors"
    >
      <svg
        class="w-5 h-5 sm:w-6 sm:h-6"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z"
        ></path>
      </svg>
    </button>
  </div>
</div>

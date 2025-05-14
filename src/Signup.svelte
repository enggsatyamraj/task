<script>
  // Form data
  let firstName = "";
  let lastName = "";
  let companyWebsite = "";
  let workEmail = "";
  let companyName = "";
  let phoneNumber = "";
  let skype = "";
  let hearAboutUs = "";
  let accountType = "advertiser"; // Default value: advertiser or brand
  let agreedToTerms = false;

  // Dropdown options
  let referralOptions = [
    "Google Search",
    "Social Media",
    "Recommendation",
    "Online Ad",
    "Conference or Event",
    "Blog or Publication",
    "Other",
  ];

  // Dropdown state
  let isDropdownOpen = false;

  function toggleDropdown() {
    isDropdownOpen = !isDropdownOpen;
  }

  function selectOption(option) {
    hearAboutUs = option;
    isDropdownOpen = false;
  }

  function handleSubmit() {
    // Validation logic would go here
    console.log("Form submitted", {
      firstName,
      lastName,
      companyWebsite,
      workEmail,
      companyName,
      phoneNumber,
      skype,
      hearAboutUs,
      accountType,
      agreedToTerms,
    });

    // Submit form logic would go here
  }
</script>

<div class="min-h-screen bg-[#fdf7e9]">
  <!-- Navigation -->
  <header class="py-4 px-6 md:px-16 lg:px-32">
    <nav class="flex justify-between items-center">
      <div>
        <a href="/" class="text-2xl font-bold">
          <img
            src="https://via.placeholder.com/150x40"
            alt="TRACKIER"
            class="h-8"
          />
        </a>
      </div>
      <div class="flex items-center space-x-4">
        <a href="/" class="text-gray-800 hover:text-gray-600">Dashboard</a>
        <a href="/#/login" class="text-gray-800 hover:text-gray-600">Login</a>
      </div>
    </nav>
  </header>

  <!-- Main Content -->
  <main class="py-12 px-6 md:px-16 lg:px-32">
    <div class="flex flex-col lg:flex-row lg:space-x-16">
      <!-- Left Column - Marketing Content -->
      <div class="lg:w-1/2 mb-10 lg:mb-0">
        <div
          class="inline-block px-4 py-2 bg-white text-blue-600 rounded-md border border-blue-100 mb-6"
        >
          30 Days Free Trial
        </div>

        <h1 class="text-4xl font-bold text-gray-900 mb-6">
          Make Data-Driven Decisions with Powerful Affiliate Marketing Software
        </h1>

        <p class="text-lg text-gray-700 mb-8">
          Get ready to turn insights into impact with real-time affiliate
          tracking.
        </p>

        <ul class="space-y-4 mb-12">
          <li class="flex items-start">
            <div
              class="flex-shrink-0 h-6 w-6 rounded-full bg-green-100 flex items-center justify-center mr-2"
            >
              <svg
                class="h-4 w-4 text-green-500"
                fill="currentColor"
                viewBox="0 0 20 20"
              >
                <path
                  fill-rule="evenodd"
                  d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
                  clip-rule="evenodd"
                ></path>
              </svg>
            </div>
            <span class="text-gray-700"
              >Seamlessly track and analyze performance across all affiliate
              campaigns.</span
            >
          </li>

          <li class="flex items-start">
            <div
              class="flex-shrink-0 h-6 w-6 rounded-full bg-green-100 flex items-center justify-center mr-2"
            >
              <svg
                class="h-4 w-4 text-green-500"
                fill="currentColor"
                viewBox="0 0 20 20"
              >
                <path
                  fill-rule="evenodd"
                  d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
                  clip-rule="evenodd"
                ></path>
              </svg>
            </div>
            <span class="text-gray-700"
              >Access a unified view of data for smarter decision-making.</span
            >
          </li>

          <li class="flex items-start">
            <div
              class="flex-shrink-0 h-6 w-6 rounded-full bg-green-100 flex items-center justify-center mr-2"
            >
              <svg
                class="h-4 w-4 text-green-500"
                fill="currentColor"
                viewBox="0 0 20 20"
              >
                <path
                  fill-rule="evenodd"
                  d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
                  clip-rule="evenodd"
                ></path>
              </svg>
            </div>
            <span class="text-gray-700"
              >Enhance profitability with real-time insights and data-driven
              strategies.</span
            >
          </li>
        </ul>

        <!-- Award badges -->
        <div class="flex flex-col">
          <div class="flex items-center mb-4">
            <div class="mr-4">
              <img
                src="https://via.placeholder.com/50"
                alt="G2 Logo"
                class="h-12 w-12"
              />
            </div>
            <div>
              <div class="flex text-yellow-400 mb-1">
                <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20">
                  <path
                    d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"
                  ></path>
                </svg>
                <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20">
                  <path
                    d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"
                  ></path>
                </svg>
                <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20">
                  <path
                    d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"
                  ></path>
                </svg>
                <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20">
                  <path
                    d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"
                  ></path>
                </svg>
                <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20">
                  <path
                    d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"
                  ></path>
                </svg>
              </div>
              <div class="text-sm font-bold">4.7 out of 5</div>
            </div>
          </div>

          <div class="flex flex-wrap gap-4">
            <div
              class="bg-white p-3 rounded-lg shadow-sm border border-gray-100 text-center w-24"
            >
              <div class="text-xs font-semibold text-orange-500">
                Easiest Setup
              </div>
              <div class="text-xs text-gray-600 mt-1">WINTER</div>
              <div class="text-sm font-bold mt-1">2024</div>
            </div>

            <div
              class="bg-white p-3 rounded-lg shadow-sm border border-gray-100 text-center w-24"
            >
              <div class="text-xs font-semibold text-purple-600">
                Best Est. ROI
              </div>
              <div class="text-xs text-gray-600 mt-1">WINTER</div>
              <div class="text-sm font-bold mt-1">2024</div>
            </div>

            <div
              class="bg-white p-3 rounded-lg shadow-sm border border-gray-100 text-center w-24"
            >
              <div class="text-xs font-semibold text-blue-500">
                Fastest Implementation
              </div>
              <div class="text-xs text-gray-600 mt-1">WINTER</div>
              <div class="text-sm font-bold mt-1">2024</div>
            </div>

            <div
              class="bg-white p-3 rounded-lg shadow-sm border border-gray-100 text-center w-24"
            >
              <div class="text-xs font-semibold text-purple-700">
                High Performer
              </div>
              <div class="text-xs text-gray-600 mt-1">WINTER</div>
              <div class="text-sm font-bold mt-1">2024</div>
            </div>
          </div>
        </div>
      </div>

      <!-- Right Column - Form -->
      <div class="lg:w-1/2">
        <div class="bg-white p-8 rounded-lg shadow-md">
          <form on:submit|preventDefault={handleSubmit} class="space-y-6">
            <!-- Name fields -->
            <div class="grid grid-cols-2 gap-4">
              <div>
                <label
                  for="firstName"
                  class="block text-sm font-medium text-gray-700 mb-1"
                >
                  First Name<span class="text-red-500">*</span>
                </label>
                <input
                  type="text"
                  id="firstName"
                  bind:value={firstName}
                  required
                  class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                  placeholder="First Name"
                />
              </div>

              <div>
                <label
                  for="lastName"
                  class="block text-sm font-medium text-gray-700 mb-1"
                >
                  Last Name<span class="text-red-500">*</span>
                </label>
                <input
                  type="text"
                  id="lastName"
                  bind:value={lastName}
                  required
                  class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                  placeholder="Last Name"
                />
              </div>
            </div>

            <!-- Company/Email fields -->
            <div class="grid grid-cols-2 gap-4">
              <div>
                <label
                  for="companyWebsite"
                  class="block text-sm font-medium text-gray-700 mb-1"
                >
                  Company Website<span class="text-red-500">*</span>
                </label>
                <input
                  type="url"
                  id="companyWebsite"
                  bind:value={companyWebsite}
                  required
                  class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                  placeholder="Company Website"
                />
              </div>

              <div>
                <label
                  for="workEmail"
                  class="block text-sm font-medium text-gray-700 mb-1"
                >
                  Work Email<span class="text-red-500">*</span>
                </label>
                <input
                  type="email"
                  id="workEmail"
                  bind:value={workEmail}
                  required
                  class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                  placeholder="Work Email"
                />
              </div>
            </div>

            <!-- Company Name -->
            <div>
              <label
                for="companyName"
                class="block text-sm font-medium text-gray-700 mb-1"
              >
                Company Name<span class="text-red-500">*</span>
              </label>
              <input
                type="text"
                id="companyName"
                bind:value={companyName}
                required
                class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                placeholder="Company Name"
              />
            </div>

            <!-- Phone Number -->
            <div>
              <label
                for="phoneNumber"
                class="block text-sm font-medium text-gray-700 mb-1"
              >
                Phone Number<span class="text-red-500">*</span>
              </label>
              <div class="flex">
                <div class="flex-shrink-0">
                  <div
                    class="flex items-center h-full px-3 py-2 border border-r-0 border-gray-300 bg-gray-50 rounded-l-md text-gray-500"
                  >
                    <span class="flex items-center">
                      <img
                        src="https://via.placeholder.com/24x16"
                        alt="India Flag"
                        class="h-4 mr-1"
                      />
                      +91
                    </span>
                  </div>
                </div>
                <input
                  type="tel"
                  id="phoneNumber"
                  bind:value={phoneNumber}
                  required
                  class="block w-full px-3 py-2 border border-gray-300 rounded-r-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                  placeholder="XXXX XXXX XX"
                />
              </div>
            </div>

            <!-- Skype -->
            <div>
              <label
                for="skype"
                class="block text-sm font-medium text-gray-700 mb-1"
              >
                Skype
              </label>
              <input
                type="text"
                id="skype"
                bind:value={skype}
                class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                placeholder="Skype"
              />
            </div>

            <!-- Where did you hear about us -->
            <div>
              <label
                for="hearAboutUs"
                class="block text-sm font-medium text-gray-700 mb-1"
              >
                Where did you hear About us?
              </label>
              <div class="relative">
                <button
                  type="button"
                  on:click={toggleDropdown}
                  class="flex justify-between w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm bg-white focus:outline-none focus:ring-blue-500 focus:border-blue-500"
                >
                  <span class="text-gray-700"
                    >{hearAboutUs || "Select an option"}</span
                  >
                  <svg
                    class="w-5 h-5 text-gray-400"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M19 9l-7 7-7-7"
                    ></path>
                  </svg>
                </button>

                {#if isDropdownOpen}
                  <div
                    class="absolute z-10 w-full mt-1 bg-white shadow-lg rounded-md py-1 max-h-60 overflow-auto"
                  >
                    {#each referralOptions as option}
                      <button
                        type="button"
                        class="block w-full px-4 py-2 text-left hover:bg-gray-100 focus:outline-none"
                        on:click={() => selectOption(option)}
                      >
                        {option}
                      </button>
                    {/each}
                  </div>
                {/if}
              </div>
            </div>

            <!-- Account Type Radios -->
            <div>
              <div class="flex items-center space-x-4">
                <div class="flex items-center">
                  <input
                    id="brand"
                    name="accountType"
                    type="radio"
                    bind:group={accountType}
                    value="brand"
                    class="h-4 w-4 text-blue-600 focus:ring-blue-500 border-gray-300"
                  />
                  <label for="brand" class="ml-2 block text-sm text-gray-700">
                    Trackier For Brands
                  </label>
                </div>

                <div class="flex items-center">
                  <input
                    id="advertiser"
                    name="accountType"
                    type="radio"
                    bind:group={accountType}
                    value="advertiser"
                    class="h-4 w-4 text-blue-600 focus:ring-blue-500 border-gray-300"
                  />
                  <label
                    for="advertiser"
                    class="ml-2 block text-sm text-gray-700"
                  >
                    Trackier For Ad Agencies / Network
                  </label>
                </div>
              </div>
            </div>

            <!-- Privacy Agreement -->
            <div class="flex items-start">
              <div class="flex items-center h-5">
                <input
                  id="terms"
                  name="terms"
                  type="checkbox"
                  bind:checked={agreedToTerms}
                  required
                  class="h-4 w-4 text-blue-600 focus:ring-blue-500 border-gray-300 rounded"
                />
              </div>
              <div class="ml-3 text-sm">
                <label for="terms" class="text-gray-700">
                  I agree to the <a
                    href="#privacy"
                    class="text-blue-600 hover:underline">Privacy Policy</a
                  > and user agreement and to receive email content from Trackier
                </label>
              </div>
            </div>

            <!-- reCAPTCHA -->
            <div class="flex items-center justify-start">
              <div
                class="g-recaptcha bg-gray-50 border border-gray-200 rounded p-2 inline-block"
              >
                <!-- This would be a real reCAPTCHA in production -->
                <div class="flex items-center">
                  <input type="checkbox" class="h-4 w-4 mr-2" />
                  <span class="text-sm">I'm not a robot</span>
                </div>
                <div class="mt-2 flex justify-between items-center">
                  <img
                    src="https://via.placeholder.com/40"
                    alt="reCAPTCHA logo"
                    class="h-8"
                  />
                  <div class="text-xs text-gray-500">
                    <div>Privacy - Terms</div>
                  </div>
                </div>
              </div>
            </div>

            <!-- Submit Button -->
            <div>
              <button
                type="submit"
                class="w-full flex justify-center py-3 px-4 border border-transparent rounded-md shadow-sm text-base font-medium text-white bg-black hover:bg-gray-800 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
              >
                SUBMIT
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </main>

  <!-- Chat Button (Fixed) -->
  <div class="fixed bottom-6 right-6">
    <button
      class="bg-indigo-900 text-white rounded-full w-16 h-16 flex items-center justify-center shadow-lg hover:bg-indigo-800 transition-colors"
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
          d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z"
        ></path>
      </svg>
    </button>
  </div>
</div>

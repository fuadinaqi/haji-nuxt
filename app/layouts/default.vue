<template>
  <div class="min-h-screen">
    <!-- Header -->
    <header class="bg-primary-light sticky top-0 z-10 w-full backdrop-blur-sm">
      <div class="container mx-auto px-4 py-3">
        <div class="flex items-center justify-between">
          <div class="flex items-center space-x-2">
            <slot name="back-button" />
            <div>
              <h1 class="text-lg font-semibold text-gray-800">Hi, John Doe</h1>
            </div>
          </div>
          <div class="flex items-center space-x-4">
            <slot name="user-profile">
              <NuxtLink to="/kepegawaian/profil">
                <button>
                  <UIcon
                    name="material-symbols:account-circle"
                    size="30"
                    class="text-primary-main"
                  />
                </button>
              </NuxtLink>
            </slot>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <main class="flex-1">
      <slot />
    </main>
  </div>
</template>

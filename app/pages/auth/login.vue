<script setup>
definePageMeta({
  layout: false,
});

// State untuk loading
const isLoading = ref(false);

// Gunakan composable useAuth
const { login } = useAuth();

// Handle SSO login
const handleSSOLogin = async () => {
  try {
    isLoading.value = true;

    // TODO: Implementasi SSO login
    console.log("SSO Login attempt");

    // Simulate SSO process
    await new Promise((resolve) => setTimeout(resolve, 1500));

    // Set autentikasi ke true
    login();

    // Success - redirect to dashboard
    navigateTo("/");
  } catch (error) {
    console.error("SSO Login error:", error);
    alert("Login SSO gagal. Silakan coba lagi.");
  } finally {
    isLoading.value = false;
  }
};
</script>

<template>
  <div
    class="from-primary-50 to-primary-100 min-h-screen bg-gradient-to-br via-white"
  >
    <!-- Background Pattern -->
    <div class="absolute inset-0 overflow-hidden">
      <div
        class="bg-primary-200 absolute -top-40 -right-40 h-80 w-80 rounded-full opacity-20"
      ></div>
      <div
        class="bg-primary-300 absolute -bottom-40 -left-40 h-80 w-80 rounded-full opacity-20"
      ></div>
    </div>

    <div
      class="relative flex min-h-screen items-center justify-center px-4 py-8"
    >
      <!-- Login Card -->
      <div class="w-full max-w-md">
        <!-- Logo & Header -->
        <div class="mb-8 text-center">
          <div
            class="bg-primary-main mx-auto mb-4 flex h-16 w-16 items-center justify-center rounded-full"
          >
            <UIcon name="lucide:building-2" class="h-8 w-8 text-white" />
          </div>
          <h1 class="text-2xl font-bold text-gray-900 sm:text-3xl">
            Selamat Datang
          </h1>
          <p class="mt-2 text-gray-600">Masuk ke sistem menggunakan SSO</p>
        </div>

        <!-- SSO Login Form -->
        <div class="rounded-2xl bg-white p-6 shadow-xl sm:p-8">
          <div class="space-y-6">
            <!-- SSO Login Button -->
            <UButton
              @click="handleSSOLogin"
              :loading="isLoading"
              :disabled="isLoading"
              color="primary"
              size="lg"
              class="w-full justify-center text-center"
            >
              <UIcon
                name="lucide:smartphone"
                class="mr-2 h-4 w-4 text-center"
              />
              {{ isLoading ? "Memproses SSO..." : "Masuk dengan SSO" }}
            </UButton>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

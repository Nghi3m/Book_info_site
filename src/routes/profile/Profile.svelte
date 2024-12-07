<script>
    import { goto } from '$app/navigation';
    export let user = null; // passed from the parent
  
    let username = user ? user.username : '';
    let currentPassword = '';
    let newPassword = '';
    let confirmPassword = '';
    let usernameError = '';
    let passwordError = '';
    let successMessage = '';
  
    // Function to handle username change
    function handleUsernameChange() {
      if (username.length < 3) {
        usernameError = 'Username must be at least 3 characters long';
        return;
      }
  
      usernameError = '';
      successMessage = 'Username updated successfully!';
      // Here you would handle the API call to update the username
      // For now, we'll assume the username is updated locally.
      user.username = username;
    }
  
    // Function to handle password change
    function handlePasswordChange() {
      if (newPassword !== confirmPassword) {
        passwordError = 'Passwords do not match';
        return;
      }
  
      if (newPassword.length < 6) {
        passwordError = 'Password must be at least 6 characters long';
        return;
      }
  
      passwordError = '';
      successMessage = 'Password updated successfully!';
      // Here you would handle the API call to update the password
      // For now, we'll simulate it by clearing the password fields
      currentPassword = '';
      newPassword = '';
      confirmPassword = '';
    }
  
    // Handle the logout functionality
    function handleLogout() {
      // Clear the user data and navigate to the home page or login page
      user = null;
      goto('/');
    }
  </script>
  
  <div class="max-w-fit mx-auto p-6">
    <h2 class="text-2xl font-semibold mb-4">Thông tin cá nhân</h2>
  
    {#if successMessage}
      <div class="bg-green-100 text-green-700 p-4 rounded mb-4">
        {successMessage}
      </div>
    {/if}
  
    <div class="bg-white shadow-md p-6 rounded-lg mb-6">
      <h3 class="text-xl font-semibold mb-4">Thay đổi tên tài khoản</h3>
      <div class="mb-4">
        <label for="username" class="block text-sm">Tên tài khoản:</label>
        <input
          type="text"
          id="username"
          bind:value={username}
          class="w-full border rounded px-2 py-1"
        />
        {#if usernameError}
          <p class="text-red-500 text-sm">{usernameError}</p>
        {/if}
      </div>
      <button
        on:click={handleUsernameChange}
        class="bg-blue-500 text-white px-4 py-2 rounded"
      >
        Lưu tên tài khoản
      </button>
    </div>
  
    <div class="bg-white shadow-md p-6 rounded-lg">
      <h3 class="text-xl font-semibold mb-4">Thay đổi mật khẩu</h3>
      <div class="mb-4">
        <label for="currentPassword" class="block text-sm">Mật khẩu hiện tại:</label>
        <input
          type="password"
          id="currentPassword"
          bind:value={currentPassword}
          class="w-full border rounded px-2 py-1"
        />
      </div>
      <div class="mb-4">
        <label for="newPassword" class="block text-sm">Mật khẩu mới:</label>
        <input
          type="password"
          id="newPassword"
          bind:value={newPassword}
          class="w-full border rounded px-2 py-1"
        />
      </div>
      <div class="mb-4">
        <label for="confirmPassword" class="block text-sm">Xác nhận mật khẩu mới:</label>
        <input
          type="password"
          id="confirmPassword"
          bind:value={confirmPassword}
          class="w-full border rounded px-2 py-1"
        />
      </div>
      {#if passwordError}
        <p class="text-red-500 text-sm">{passwordError}</p>
      {/if}
      <button
        on:click={handlePasswordChange}
        class="bg-blue-500 text-white px-4 py-2 rounded"
      >
        Lưu mật khẩu
      </button>
    </div>
  
    <button
      on:click={handleLogout}
      class="mt-6 bg-red-500 text-white px-4 py-2 rounded"
    >
      Đăng xuất
    </button>
  </div>
  
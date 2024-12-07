<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
  
    function closeModal() {
      dispatch('close');
    }
  </script>
  
  <div class="fixed inset-0 bg-gray-800 bg-opacity-50 flex justify-center items-center z-20">
    <div class="bg-white rounded shadow-md p-8 w-96 relative">
      <h2 class="text-lg font-bold text-blue-600 mb-4">ĐĂNG NHẬP</h2>
      <form class="space-y-4">
        <div>
          <label class="block text-gray-700">Tên tài khoản</label>
          <input type="text" class="border rounded w-full px-3 py-2" />
        </div>
        <div>
          <label class="block text-gray-700">Mật khẩu</label>
          <input type="password" class="border rounded w-full px-3 py-2" />
        </div>
        <div class="flex justify-between">
          <button type="button" class="bg-blue-600 text-white px-4 py-2 rounded">Xác Nhận</button>
          <button type="button" class="bg-gray-300 px-4 py-2 rounded" on:click={closeModal}>
            Hoàn tác
          </button>
        </div>
      </form>
      <div class="flex justify-between mt-4 text-blue-600">
        <a href="#" class="hover:underline">Đăng kí</a>
        <a href="#" class="hover:underline">Quên mật khẩu</a>
      </div>
    </div>
  </div>
  
<script>
    export let toggleLoginModal;
  </script>
  
  <nav class="bg-blue-600 text-white fixed top-0 w-full z-10 shadow-md">
    <div class="container mx-auto flex justify-between items-center py-4 px-6">
      <div class="text-xl font-bold">BKBOOKS</div>
      <ul class="flex space-x-6">
        <li><a href="#" class="hover:underline">Trang chủ</a></li>
        <li><a href="#" class="hover:underline">Xếp hạng</a></li>
        <li><a href="#" class="hover:underline">Thể loại</a></li>
        <li><a href="#" class="hover:underline">Báo cáo</a></li>
        <li><a href="#" class="hover:underline">Thông tin</a></li>
        <li><a href="#" class="hover:underline">Fanpage</a></li>
      </ul>
      <div class="space-x-4">
        <button class="bg-blue-700 px-4 py-2 rounded text-white" on:click={toggleLoginModal}>
          Đăng nhập
        </button>
        <button class="bg-blue-800 px-4 py-2 rounded text-white">Đăng kí</button>
      </div>
    </div>
  </nav>
  <div class="h-16"></div> <!-- Spacer for navbar height -->
  
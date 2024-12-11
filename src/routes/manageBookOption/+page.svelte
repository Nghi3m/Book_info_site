<script>
  import { goto } from '$app/navigation';

  let currentPage = 1;
  let totalPages = 5;
  let books = Array(10).fill().map((_, i) => ({
    id: Math.random().toString(36).substr(2, 9),
    title: `Thanh Gươm Diệt Quỷ ${i + 1}`,
    chapter: `Chap ${200 + i + 1}`,
    cover: "/path/to/cover.jpg",
  }));
  let deleteMode = false;

  function goToPage(page) {
    if (page >= 1 && page <= totalPages) {
      currentPage = page;
    }
  }

  function editBook(bookId) {
    goto(`/editBook?bookId=${bookId}`);
  }

  function toggleDeleteMode() {
    deleteMode = !deleteMode;
  }

  function deleteBook(bookId) {
    books = books.filter(book => book.id !== bookId);
  }
</script>

<div class="bg-blue-50 min-h-screen p-4">
<header class="bg-blue-600 text-white p-4 rounded-md flex justify-between items-center">
  <h1 class="text-xl font-bold">BKBOOKS</h1>
<button class="bg-white text-blue-700 rounded py-2 px-4"
    on:click={()=>goto("/")}>Quay lại</button>
</header>

<div class="flex mt-6">
  <!-- Sidebar -->
  <nav class="w-1/5 bg-blue-700 text-white rounded-md p-4">
    <ul class="space-y-4">
      <li><a href="#" class="block hover:bg-blue-600 p-2 rounded bg-blue-800">Quản Lý Sách</a></li>
      <li><a href="#" class="block hover:bg-blue-600 p-2 rounded">Quản Lý Tài Khoản</a></li>
      <li><a href="#" class="block hover:bg-blue-600 p-2 rounded">Thống kê lượt xem</a></li>
    </ul>
  </nav>

  <!-- Main Content -->
  <main class="w-4/5 bg-white rounded-md p-6 ml-4">
    <h2 class="text-2xl font-bold text-gray-700">Tủ Sách Hiện Tại</h2>

    <!-- Search and Buttons -->
    <div class="mt-4 flex items-center gap-4">
      <input
        type="text"
        placeholder="Tìm kiếm theo tên hoặc id Sách"
        class="border border-gray-300 rounded-md p-2 flex-1"
      />
      <button class="px-4 py-2 bg-green-500 text-white rounded hover:bg-green-600"
        on:click={()=>goto("/addBook")}>Thêm Sách</button>
      <button class="px-4 py-2 bg-red-500 text-white rounded hover:bg-red-600" on:click={toggleDeleteMode}>
        {deleteMode ? 'Xong' : 'Xóa sách'}
      </button>
    </div>

    <!-- Book List -->
    <div class="grid grid-cols-4 gap-6 mt-6">
      {#each books as book}
        <div 
          class="border rounded-md shadow-md p-4 text-center hover:shadow-lg transition cursor-pointer" 
          class:bg-red-100={deleteMode}
          on:click={() => deleteMode ? deleteBook(book.id) : editBook(book.id)}>
          <img src={book.cover} alt={book.title} class="w-full h-40 object-cover rounded-md" />
          <h3 class="mt-2 text-gray-700 font-semibold">{book.title}</h3>
          <p class="text-gray-500">{book.chapter}</p>
        </div>
      {/each}
    </div>

    <!-- Pagination -->
    <div class="mt-6 flex justify-center items-center gap-2">
      {#each Array(totalPages) as _, i}
        <button
          class="px-4 py-2 border rounded-md text-gray-700 hover:bg-gray-100"
          class:bg-blue-600={currentPage === i + 1}
          class:text-white={currentPage === i + 1}
          on:click={() => goToPage(i + 1)}
        >
          {i + 1}
        </button>
      {/each}
    </div>
  </main>
</div>
</div>

<style>
/* Add custom styles if necessary */
</style>

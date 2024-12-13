<script>
  import { onMount } from 'svelte';
  import { page } from '$app/stores';
  import { goto } from '$app/navigation';

  let book = null;
  let bookId = null;
  let userId = 'U0000001'; // Static userId for this example
  let isLiked = false;
  let isFollowing = false;

  // Parse the bookId from URL
  $: bookId = $page.url.searchParams.get('bookId');

  async function fetchBookDetails() {
    if (!bookId) return;

    try {
      const response = await fetch(`http://localhost:3000/getBookDetails?bookId=${bookId}&userId=${userId}`);
      const data = await response.json();

      if (data.success) {
        book = data.book;
        isLiked = book.isFavorite === 1;
        isFollowing = book.totalFollowers > 0;
      } else {
        console.error('Failed to fetch book details');
      }
    } catch (error) {
      console.error('Error fetching book details:', error);
    }
  }

  function toggleLike() {
    isLiked = !isLiked;
    // Handle API request to update favorite status
  }

  function toggleFollow() {
    isFollowing = !isFollowing;
    // Handle API request to update follow status
  }

  onMount(fetchBookDetails);
</script>

{#if book}
<div class="bg-blue-50 min-h-screen p-4">
  <div class="max-w-4xl mx-auto bg-white rounded-lg shadow-md p-6 mt-20">
    <header class="flex justify-between items-center mb-4">
      <h1 class="text-2xl font-bold text-blue-600">{book.title}</h1>
      <button class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600" on:click={() => goto('/')}>Quay Lại</button>
    </header>

    <div class="flex gap-4">
      <!-- Cover Image -->
      <img src={"covers/" + book.coverPath} class="w-32 h-40 rounded-md" alt="Book Cover" />

      <!-- Book Details -->
      <div class="flex-1">
        <p class="text-gray-600">Tác giả: <span class="font-semibold">{book.author}</span></p>
        <div class="mt-3">
          <p class="text-gray-600">Lượt thích: <span class="font-semibold">{book.totalFavorites || 0}</span></p>
          <p class="text-gray-600">Người đọc: <span class="font-semibold">{book.totalReaders || 0}</span></p>
          <p class="text-gray-600">Lượt theo dõi: <span class="font-semibold">{book.totalFollowers}</span></p>
        </div>

        <div class="mt-4 flex flex-wrap gap-2">
          {#each book.categories as category}
            <span class="px-3 py-1 bg-blue-100 text-blue-600 rounded-full text-sm">{category}</span>
          {/each}
        </div>

        <div class="mt-6 flex gap-4">
          <button
            class="px-4 py-2 bg-blue-600 text-white rounded hover:bg-blue-700"
            on:click={() => {}}
          >
            Bắt Đầu Đọc
          </button>
          <button
            class="px-4 py-2 border rounded text-gray-700 hover:bg-gray-100"
            class:is-liked={isLiked}
            on:click={toggleLike}
          >
            {isLiked ? 'Đã Thích' : 'Thích'}
          </button>
          <button
            class="px-4 py-2 border rounded text-gray-700 hover:bg-gray-100"
            class:is-following={isFollowing}
            on:click={toggleFollow}
          >
            {isFollowing ? 'Đang Theo Dõi' : 'Theo Dõi'}
          </button>
        </div>
      </div>
    </div>

    <!-- Book Description -->
    <div class="mt-8">
      <h2 class="text-lg font-semibold text-gray-800">Thông Tin Sách</h2>
      <p class="mt-2 text-gray-600">{book.description || 'Không có mô tả.'}</p>
    </div>
  </div>
</div>
{:else}
<div class="flex items-center justify-center min-h-screen">
  <p class="text-gray-500">Đang tải...</p>
</div>
{/if}

<style>
  /* Add custom styles if needed */
</style>

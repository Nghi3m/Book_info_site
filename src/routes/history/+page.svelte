<script>
    import { goto } from '$app/navigation';

    let username = "MeTruyen123";
    let books = Array(12).fill().map((_, i) => ({
        id: Math.random().toString(36).substr(2, 9),
        title: `Thanh Gươm Diệt Quỷ`,
        chapter: `Chap 206`,
        cover: "/path/to/cover.jpg",
    }));
    let currentPage = 1;
    let totalPages = 5;

    function goToPage(page) {
        if (page >= 1 && page <= totalPages) {
            currentPage = page;
        }
    }

    function clearHistory() {
        if (confirm("Bạn có chắc chắn muốn xóa toàn bộ lịch sử?")) {
            books = [];
        }
    }

    function goBack() {
        goto("/");
    }
</script>

<div class="bg-blue-50 min-h-screen p-6">
    <header class="flex justify-between items-center mb-4">
        <h1 class="text-xl font-bold text-gray-700">Lịch sử người dùng: <span class="text-blue-600">{username}</span></h1>
        <button class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600" on:click={goBack}>
            Quay Lại
        </button>
    </header>

    <div class="bg-white p-4 rounded-md shadow-md">
        <button class="px-4 py-2 bg-red-500 text-white rounded hover:bg-red-600 mb-4" on:click={clearHistory}>
            Xóa Lịch Sử
        </button>

        <div class="grid grid-cols-4 gap-4">
            {#each books as book}
                <div class="border rounded-md shadow-md p-4 text-center hover:shadow-lg transition">
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
    </div>
</div>

<style>
    /* Add custom styles if necessary */
</style>

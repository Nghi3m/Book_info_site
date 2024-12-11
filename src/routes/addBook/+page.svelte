<script>
    import { goto } from '$app/navigation';

    let bookTitle = "";
    let author = "";
    let bookId = "";
    let selectedCategory = "";
    let categories = ["Shounen", "Tragedy", "Drama", "Historical"];
    let tags = [];
    let coverImage = null;
    let coverPreview = "";

    function addTag(tag) {
        if (tag && !tags.includes(tag)) {
            tags = [...tags, tag];
        }
    }

    function removeTag(tag) {
        tags = tags.filter(t => t !== tag);
    }

    function handleImageUpload(event) {
        const file = event.target.files[0];
        if (file) {
            coverImage = file;
            const reader = new FileReader();
            reader.onload = () => {
                coverPreview = reader.result;
            };
            reader.readAsDataURL(file);
        }
    }

    async function saveBook() {
        if (!bookTitle || !author || !bookId) {
            alert("Vui lòng điền đầy đủ thông tin sách.");
            return;
        }

        const formData = new FormData();
        formData.append("title", bookTitle);
        formData.append("author", author);
        formData.append("bookId", bookId);
        formData.append("tags", JSON.stringify(tags));
        if (coverImage) {
            formData.append("cover", coverImage);
        }

        try {
            const response = await fetch("/api/save-book", {
                method: "POST",
                body: formData,
            });

            if (response.ok) {
                alert("Sách đã được lưu thành công.");
                goto("/");
            } else {
                alert("Đã xảy ra lỗi khi lưu sách.");
            }
        } catch (error) {
            console.error("Error saving book:", error);
            alert("Đã xảy ra lỗi khi lưu sách.");
        }
    }

    function goBack() {
        goto("/manageBookOption");
    }
</script>

<div class="bg-blue-50 min-h-screen p-6">
    <header class="flex justify-between items-center mb-4">
        <h1 class="text-2xl font-bold text-blue-600">Thêm Sách Mới</h1>
        <button class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600" on:click={goBack}>
            Quay Lại
        </button>
    </header>

    <div class="bg-white p-6 rounded-md shadow-md">
        <div class="flex gap-6">
            <!-- Image Section -->
            <div class="flex flex-col items-center justify-center w-1/3">
                <div class="w-full h-48 bg-gray-200 flex items-center justify-center rounded relative">
                    {#if coverPreview}
                        <img src={coverPreview} alt="Cover Preview" class="w-full h-full object-cover rounded" />
                    {:else}
                        <span class="text-gray-500">Thêm hình ảnh</span>
                    {/if}
                    <input
                        type="file"
                        accept="image/*"
                        class="absolute inset-0 opacity-0 cursor-pointer"
                        on:change={handleImageUpload}
                    />
                </div>
            </div>

            <!-- Input Fields -->
            <div class="flex-1 space-y-4">
                <div>
                    <label class="block text-gray-700 font-semibold">Tên Truyện - Sách:</label>
                    <input
                        type="text"
                        bind:value={bookTitle}
                        placeholder="Điền tên Truyện - Sách"
                        class="border border-gray-300 rounded-md w-full p-2"
                    />
                </div>
                <div>
                    <label class="block text-gray-700 font-semibold">Tác giả:</label>
                    <input
                        type="text"
                        bind:value={author}
                        placeholder="Điền tên Tác Giả"
                        class="border border-gray-300 rounded-md w-full p-2"
                    />
                </div>
                <div>
                    <label class="block text-gray-700 font-semibold">Mã Sách:</label>
                    <input
                        type="text"
                        bind:value={bookId}
                        placeholder="Điền mã sách"
                        class="border border-gray-300 rounded-md w-full p-2"
                    />
                </div>
                <div>
                    <label class="block text-gray-700 font-semibold">Thể loại:</label>
                    <select
                        bind:value={selectedCategory}
                        class="border border-gray-300 rounded-md w-full p-2"
                        on:change={(e) => addTag(e.target.value)}
                    >
                        <option value="" disabled>Chọn thể loại</option>
                        {#each categories as category}
                            <option value={category}>{category}</option>
                        {/each}
                    </select>
                </div>
            </div>
        </div>

        <!-- Tag List -->
        <div class="mt-6">
            <h3 class="text-gray-700 font-semibold">Các Tag hiện có:</h3>
            <div class="flex flex-wrap gap-2 mt-2">
                {#each tags as tag}
                    <div class="flex items-center bg-blue-100 text-blue-700 px-4 py-2 rounded-full shadow-md">
                        <span>{tag}</span>
                        <button
                            class="ml-2 text-red-500 hover:text-red-700"
                            on:click={() => removeTag(tag)}
                        >
                            &times;
                        </button>
                    </div>
                {/each}
            </div>
        </div>

        <!-- Save Button -->
        <div class="mt-6 flex justify-end">
            <button class="px-6 py-2 bg-blue-500 text-white rounded hover:bg-blue-600" on:click={saveBook}>
                Xác nhận
            </button>
        </div>
    </div>
</div>

<style>
    /* Add any additional styling if needed */
</style>

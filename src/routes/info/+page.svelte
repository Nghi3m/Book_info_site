<script>
    import Navbar from '../../components/NavBar.svelte';
    import LoginModal from '../../components/LoginModal.svelte';
	import Category from '../../components/Category.svelte';
	import { goto } from '$app/navigation';

    let showLoginModal = false;
    let isAuthenticated = false;
    const nullUser = {"username":null, "profilePic":null};
    let user = nullUser;

    const item = {"image": 'thumbnails/kimetsunoyaiba.png',"title": "Thanh Gươm Diệt Quỷ" ,"category":["Shounen", "Tragedy", "Drama", "Historical"], "author": "Gotouge Koyoharu", "status": "Đã hoàn thành", "fav":20000000,"view":10000000 ,"fol":100000, "desc":"Kismetu no Yaiba – Tanjirou là con cả của gia đình vừa mất cha. Một ngày nọ, Tanjirou đến thăm thị trấn khác để bán than, khi đêm về cậu ở nghỉ tại nhà người khác thay vì về nhà vì lời đồn thổi về ác quỷ luôn rình mò gần núi vào buổi tối. Khi cậu về nhà vào ngày hôm sau, bị kịch đang đợi chờ cậu…"}

    function toggleLoginModal() {
    showLoginModal = !showLoginModal;
  }
    /**
	 * @param {any} loggedinUser
	 */
    function handleLoginSuccess(loggedinUser) {
        isAuthenticated = true;
        user = loggedinUser;
        showLoginModal = false;
    }

    function logout() {
        isAuthenticated = false;
        user = nullUser;
    }

    let isLiked = false;
  let isFollowing = false;

  function toggleLike() {
    isLiked = !isLiked;
  }

  function toggleFollow() {
    isFollowing = !isFollowing;
  }
</script>

<div class="bg-blue-50 min-h-screen p-4">
  <div class="max-w-4xl mx-auto bg-white rounded-lg shadow-md p-6 mt-20">
    <header class="flex justify-between items-center mb-4">
        <h1 class="text-2xl font-bold text-blue-600">{item.title}</h1>
        <button class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600" on:click={()=>goto("/")}>
            Quay Lại
        </button>
    </header>
    <div class="flex gap-4">
      <!-- Cover Image -->
      <img
        src={item.image}
        class="w-32 h-40 rounded-md"
      />

      <!-- Book Details -->
      <div class="flex-1">
        <p class="text-gray-600">Tác giả: <span class="font-semibold">{item.author}</span></p>
        <p class="text-gray-600">Tình trạng: <span class="font-semibold">{item.status}</span></p>

        <div class="mt-3">
          <p class="text-gray-600">Lượt thích: <span class="font-semibold">{item.fav}</span></p>
          <p class="text-gray-600">Lượt xem: <span class="font-semibold">{item.view}</span></p>
          <p class="text-gray-600">Lượt theo dõi: <span class="font-semibold">{item.fol}</span></p>
        </div>

        <div class="mt-4 flex flex-wrap gap-2">
            {#each item.category as category}   
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
      <p class="mt-2 text-gray-600">
        {item.desc}
      </p>
    </div>
  </div>
</div>

<style>
  /* Add custom styles if needed */
</style>

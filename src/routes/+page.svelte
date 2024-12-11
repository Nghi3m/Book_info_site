<script>
    import Navbar from '../components/NavBar.svelte';
    import Section from '../components/Section.svelte';
    import LoginModal from '../components/LoginModal.svelte';

    let showLoginModal = false;
    let isAuthenticated = false;
    const nullUser = {"username":null, "profilePic":null};
    let user = nullUser;

    const items = Array(8).fill({
      title: 'Thanh Gươm Diệt Quỷ',
      image: 'thumbnails/kimetsunoyaiba.png', // Replace with your image path
    });

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
</script>
<Navbar
  isAuthenticated={isAuthenticated}
  user={user}
  onLogin={toggleLoginModal}
  onLogout={logout}
/>

<main class="bg-blue-100 py-32 max-w-full">
  <Section title="Truyện mới nhất" items={items} />
  <Section title="Lượt xem nhiều nhất" items={items} />
</main>

{#if showLoginModal}
<LoginModal 
    on:loginSuccess={(e) => handleLoginSuccess(e.detail)} 
    on:close={()=>{showLoginModal=false}}/>

{/if}

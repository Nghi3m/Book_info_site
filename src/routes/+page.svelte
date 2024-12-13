<script>
  import { onMount } from 'svelte';
  import Navbar from '../components/NavBar.svelte';
  import Section from '../components/Section.svelte';
  import LoginModal from '../components/LoginModal.svelte';

  let showLoginModal = false;
  let isAuthenticated = false;
  const nullUser = { "username": null, "profilePic": null };
  let user = nullUser;
  let books = []; // Store books fetched from the API

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

  // Fetch books from API
  onMount(async () => {
      try {
          const response = await fetch('http://localhost:3000/getAllbooks');
          const data = await response.json();
          if (data.success) {
              books = data.books.map(book => ({
                  bookId: book.book_id,
                  title: book.title,
                  image: "covers/" + book.cover_path, // Assuming file_path contains the thumbnail or placeholder
                  author: book.author,
              }));
          }
      } catch (error) {
          console.error('Failed to fetch books:', error);
      }
  });
</script>

<Navbar
isAuthenticated={isAuthenticated}
user={user}
onLogin={toggleLoginModal}
onLogout={logout}
/>

<main class="bg-blue-100 py-32 max-w-full">
<Section title="Truyện mới nhất" items={books} />
<Section title="Lượt xem nhiều nhất" items={books} />
</main>

{#if showLoginModal}
<LoginModal 
  on:loginSuccess={(e) => handleLoginSuccess(e.detail)} 
  on:close={() => { showLoginModal = false }} 
/>
{/if}

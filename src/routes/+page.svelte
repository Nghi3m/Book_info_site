<script>
    import Navbar from '../components/Navbar.svelte';
    import Section from '../components/Section.svelte';
    import LoginModal from '../components/LoginModal.svelte';

    let showLoginModal = false;
    const items = Array(8).fill({
      title: 'Thanh Gươm Diệt Quỷ',
      chapter: 'Chap 206',
      image: 'thumbnails/kimetsunoyaiba.png', // Replace with your image path
    });

    function toggleLoginModal() {
    showLoginModal = !showLoginModal;
  }
</script>
<Navbar {toggleLoginModal} />
<main class="bg-blue-100 py-8">
  <Section title="Truyện mới nhất" items={items} />
  <Section title="Lượt xem nhiều nhất" items={items} />
</main>
{#if showLoginModal}
  <LoginModal on:close={toggleLoginModal} />
{/if}

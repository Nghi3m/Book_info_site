<script>
    import Profile from './Profile.svelte';
    import { user } from '../../stores/userStore.js';

    let userProfile = $user;
  </script>
  
  <Profile {userProfile} />
  
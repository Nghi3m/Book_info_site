<script>
    import {goto} from "$app/navigation"
    export let item;
  </script>
  
  <div class="bg-white shadow rounded overflow-hidden cursor-pointer"
    on:click={()=>{goto("/info?bookId="+item.bookId)}}>
    <img src={item.image} alt={item.title} class="w-fit h-50 object-cover" />
    <div class="p-4">
      <h3 class="text-base font-bold">{item.title}</h3>
    </div>
  </div>
  
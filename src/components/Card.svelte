<script>
    export let item;
  </script>
  
  <div class="bg-white shadow rounded overflow-hidden">
    <img src={item.image} alt={item.title} class="w-full h-40 object-cover" />
    <div class="p-4">
      <h3 class="text-base font-bold">{item.title}</h3>
      <p class="text-sm text-gray-600">{item.chapter}</p>
    </div>
  </div>
  
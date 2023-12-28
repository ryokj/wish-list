<script lang="ts">
  type Item = {
    id: string;
    name: string;
  };

  let id = 0;
  let itemName: string = '';
  let wishList: Item[] = [
    { id: `dummy-id-${++id}`, name: 'Apple' },
    { id: `dummy-id-${++id}`, name: 'Orange' }
  ];

  function addItem() {
    if (itemName === '') return;
    wishList = [...wishList, { id: `dummy-id-${++id}`, name: itemName }];
    itemName = '';
  }

  function delItem(item: Item) {
    wishList = wishList.filter((v) => v.id !== item.id);
  }
</script>

<section class="flex justify-center">
  <div class="border rounded m-10 p-10 space-y-5 w-[600px]">
    <h1 class="text-3xl font-bold">✅ Wish List</h1>
    <div class="flex space-x-2">
      <input
        type="text"
        bind:value={itemName}
        class="border border-gray-500 rounded py-1 px-2 grow"
      />
      <button on:click={addItem} class="border border-gray-500 rounded bg-gray-200 py-1 px-2"
        >Add Item</button
      >
    </div>
    <ul class="space-y-2">
      {#each wishList as item (item.id)}
        <li
          class="flex justify-between border border-gray-200 py-1 px-2 space-x-2 rounded hover:bg-orange-100"
        >
          <p class="flex space-x-2"><span>✔</span><span>{item.name}</span></p>
          <button on:click={() => delItem(item)}>🗑️</button>
        </li>
      {/each}
    </ul>
  </div>
</section>

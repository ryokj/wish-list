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

<section>
  <div>
    <h1>✅ Wish List</h1>
    <div>
      <input type="text" bind:value={itemName} />
      <button on:click={addItem}>Add Item</button>
    </div>
    <ul>
      {#each wishList as item (item.id)}
        <li>
          <p><span>✔</span><span>{item.name}</span></p>
          <button on:click={() => delItem(item)}>🗑️</button>
        </li>
      {/each}
    </ul>
  </div>
</section>

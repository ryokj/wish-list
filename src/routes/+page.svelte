<script lang="ts">
  type Item = {
    name: string;
  };

  let itemName: string = '';
  let wishList: Item[] = [{ name: 'Apple' }, { name: 'Orange' }];

  function addItem() {
    if (itemName === '') return;
    wishList = [...wishList, { name: itemName }];
    itemName = '';
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
      {#each wishList as item}
        <li>
          <p><span>✔</span><span>{item.name}</span></p>
          <button>🗑️</button>
        </li>
      {/each}
    </ul>
  </div>
</section>

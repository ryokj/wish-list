<script lang="ts">
  type Item = {
    name: string;
  };

  let wishList: Item[] = [{ name: 'Apple' }, { name: 'Orange' }];
</script>

<section>
  <div>
    <h1>✅ Wish List</h1>
    <div>
      <input type="text" />
      <button>Add Item</button>
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

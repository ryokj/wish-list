<script lang="ts">
  import {
    addDoc,
    collection,
    onSnapshot,
    query,
    QuerySnapshot,
    serverTimestamp,
    FieldValue,
    orderBy,
    deleteDoc,
    doc,
    type DocumentData
  } from 'firebase/firestore';
  import { db } from '$lib/firebase';

  type Item = {
    id?: string;
    name: string;
    timestamp: FieldValue;
  };

  let itemName: string = '';
  let wishList: Item[] = [];

  function addItem() {
    if (itemName === '') return;
    const item: Item = {
      name: itemName,
      timestamp: serverTimestamp()
    };
    addDoc(collection(db, 'wishlist'), item);
    itemName = '';
  }

  function delItem(item: Item) {
    if (!item.id) return;
    deleteDoc(doc(db, 'wishlist', item.id));
  }

  onSnapshot(
    query(collection(db, 'wishlist'), orderBy('timestamp', 'desc')),
    (snapshot: QuerySnapshot) => {
      wishList = snapshot.docs.map((doc) => {
        const data: DocumentData = doc.data();
        const item: Item = {
          id: doc.id,
          name: data.name,
          timestamp: data.timestamp
        };
        return item;
      });
    }
  );
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

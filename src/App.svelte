<script lang="ts">
  import svelteLogo from './assets/svelte.svg'
  import Counter from './lib/Counter.svelte';


import * as Automerge from "@automerge/automerge"

function Encodeuint8arr(myString){
    return new TextEncoder("utf-8").encode(myString);
}

function Decodeuint8arr(uint8array){
    return new TextDecoder("utf-8").decode(uint8array);
}

let doc1 = Automerge.init()
console.log(doc1)
doc1 = Automerge.change(doc1, 'Add card', doc => {
  doc.cards = []
  doc.cards.push({ title: 'Rewrite everything in Clojure', done: false })
  doc.cards.push({ title: 'Rewrite everything in Haskell', done: false })
})

const a = Automerge.save(doc1);
console.warn({a});

localStorage.setItem('miGato', a.toString());

let newDoc = Automerge.load(Uint8Array.from(localStorage.getItem('miGato').split(',').map(x=>parseInt(x,10))))

console.log(newDoc)

// console.log("aca");
// console.warn({ c});

// console.log(Automerge.getHistory(doc1).map(state => [state.change.message, state.snapshot.cards.length]))

</script>

<main>
  <div>
    <a href="https://vitejs.dev" target="_blank" rel="noreferrer"> 
      <img src="/vite.svg" class="logo" alt="Vite Logo" />
    </a>
    <a href="https://svelte.dev" target="_blank" rel="noreferrer"> 
      <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
    </a>
  </div>
  <h1>Vite + Svelte</h1>

  <div class="card">
    <Counter />
  </div>

  <p>
    Check out <a href="https://github.com/sveltejs/kit#readme" target="_blank" rel="noreferrer">SvelteKit</a>, the official Svelte app framework powered by Vite!
  </p>

  <p class="read-the-docs">
    Click on the Vite and Svelte logos to learn more
  </p>
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style>
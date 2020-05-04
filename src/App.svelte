<script>
  export let name;
  let word = "piano";
  let words = ["one", "two", "three"];

  //return array of booleans for matching characters
  //e.g., "yes" and "yas" returns [true, false, true]
  let compare = function*(source, target) {
    let i = 0;

    while (i < target.length) {
      yield { match: source[i] == target[i], item: target[i] };
      i++;
    }
  };

  let generateArray = function(generatorFn, ...args) {
    return [...generatorFn(...args)];
  };
</script>

<main>
  <input type="text" bind:value={name} />
  <div>{name}</div>

  <h2>{word}</h2>
  {name == word ? 'Match' : 'Keep Trying'}
  {#each words as word}
    <div>
      {#each generateArray(compare, name, word) as letter}
        <span style="color: {letter.match ? 'red' : 'black'}">
          {letter.item}
        </span>
      {/each}
    </div>
  {/each}
</main>

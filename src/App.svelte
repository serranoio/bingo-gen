<script lang="ts">

let squares = ["Dad mocks weed smokers with retarded face",
 "Ewy mentions Gloria shouldn't have never came last year",
  "Mom shits on shroom girl",
  "Michael shits on eric",
  "Leseldie Drama",
  "Ewy says Dewy is too cocky",
  "Mom talks about her paintaing",
  "Ewy overdrinks",
  "Reddit mentioned",
  "Ewy talks about his girl",
  "Cnn Mentioned",
  "Herbalife mentioned",
  "Ewy flexes his turkey",
  "Dad flexes Dewy's salary",
  "Ewy mentions that both our girls are cosmotology majors",
  "AJ & lydia mentioned",
  "Mom gets too drunk",
  "Mom preoccupies herself over Ewy drinking",
  "Boiii!",
  "Gurllll!",
  "Michael rolls his eyes",
  "Mom overparents",
  "Roxana slays the house down boots purr",
  "Ewy & dewy wrestle",
  "One eggie became 2 eggies",
  "Ewy zyns",
  "Mom overparents again",
  "Michael shits on capitalism",
  "Dad asks 'hows school' to michael",
  "Roxana says 'im not that hungry we just ate today' and doesnt eat anymore",
  "Mom asks how their Thanksgiving went",
  "Mr Ramirez gambles?",
  "Ewy tries speaking gringo Spanish",
  ]

function shuffle(array) {
  let currentIndex = array.length,  randomIndex;

  // While there remain elements to shuffle.
  while (currentIndex > 0) {

    // Pick a remaining element.
    randomIndex = Math.floor(Math.random() * currentIndex);
    currentIndex--;

    // And swap it with the current element.
    [array[currentIndex], array[randomIndex]] = [
      array[randomIndex], array[currentIndex]];
  }

  return array;
}


  shuffle(squares)

  squares = squares.slice(0,24);

  
</script>

<main>
  <div class="grid">

    {#each squares as square}
      <div class="square">
        <div>
          {square}
        </div>
      </div>
    {/each}

    <div class="square free">
      <div>
        Free
      </div>
    </div>
    
  </div>
</main>

<style>
 main {
  max-width: 130rem;
  margin: 0 auto;
 }
 .grid {
  /* width: 100vw; */
  height: 100lvh;
  grid-template-columns: repeat(5, 1fr);
  grid-template-rows: repeat(5, 1fr);
  display: grid;
 }

 .square {
  box-shadow: 0 0 0 2px black;
 }

 .square div {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
 }

 .square.free {
  grid-column: 3/4;
  grid-row: 3/4;
 }
</style>

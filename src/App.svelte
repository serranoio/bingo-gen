<script lang="ts">
import { onMount } from "svelte";


interface Theme {
  name: string,
  squares: string[],
}

enum ThemeTypes {
  Thanksgiving = "Thanksgiving",
  Christmas = "Christmas",
  Vacation = "Vacation",
}

let selectedTheme: ThemeTypes = ThemeTypes.Thanksgiving;


if (!localStorage.getItem("selectedTheme")) {
  localStorage.setItem("selectedTheme", selectedTheme);
}

const Themes: Theme[] = [{
  name: ThemeTypes.Thanksgiving,
  squares: ["Dad mocks weed smokers with retarded face",
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
  "Roxana rolls her eyes",
  "Michael Roxana flirt",
  "michael roxana do gay shit",
  "Roxana slays the house down boots purr",
  "Ewy & dewy wrestle",
  "One eggie became 2 eggies",
  "Mom overparents",
  "Mom overparents again",
  "Michael shits on capitalism",
  "Dad asks 'hows school' to michael",
  "Roxana says 'im not that hungry we just ate today' and doesnt eat anymore",
  "Mom asks how their Thanksgiving went",
  "Mr Ramirez gambles?",
  "Ewy tries speaking gringo Spanish",
  "Moustache Mentioned",
  "David shits on somebody",
  "David brings up success",
  "MCHHHHE",
  "Mom complains about the bingo card",
  "Mom gets offended by the bingo card",
  "where are the Webbs at?",
  "Roxana gives side eye",
  "Roxana gets embarrassed or shy",
  "DONT BE GAY",
  "DONT BE DUMB",
  "Mom interrupts argument",
  "michael trashes mom", 
  "mom says idgaf",
  "mom starts dancing",
  "el grito is mentioned",
  "when eric mentions nicotine",
  "DA",
  "SAY DABOO",
  "Bobs",
],

},
{
  name: ThemeTypes.Christmas,
  squares: ["Dad complains about Israel showing off", 
  "Dad complains about Isreal showing off again",
  "Shrooms girl",
  "Ewy talks about his work when no one asked",
  "Ewy begs family to use telescope",
  "ewy hits penjamin",
  "mewy hits penjamin",
  "roxy hits penjamin",
  "aosijdaio0sjdaosidjaoisjdaoisjdcAOISDjcosdjfs0oidjfsao0j0ij",
], 
},
{
  name: ThemeTypes.Vacation, 
  squares: ["Michael shits on vacation and says he doesnt wanna go",
"mom tells Michael to be grateful",
"Ewy asks for penji",
"David Wanders",
"Michael or eric sneaks drugs on the plane",
"Ewy looks for drugs at vacation spot",
"Michael calls Roxana",
"Dad brings booze",
"Mom gets offended or upset",
"Michael peer pressures eric",
"David whines about dinner time",
"Michael finishes his food last",
"Michael takes a shit with his phone and texts bubby",
"Michael misses bubby"]
},

]


let squares = setSquares();

function setSquares() {
    return Themes.find((theme: Theme) => theme.name === selectedTheme)?.squares; 
}
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

const refreshClicked = () => { return new Array(25).map(() => "") }

let allClicked = refreshClicked(); 

// const FreeSpot = "Free Spot"
const refreshBoard = (setStorage: boolean) => {
  shuffle(squares)
  squares = squares.slice(0,25);
  allClicked = refreshClicked();

  if (setStorage) {
    localStorage.setItem("squares", JSON.stringify(squares));
  }
} 

refreshBoard(false)
  
  const onClick = (e: any) => {                
    const selected = e.target.classList.contains("square") ? e.target : e.target.closest(".square");
    console.log("set")
    console.log(allClicked)

    if (allClicked[selected.id] === "selected") {
      allClicked[selected.id] = ""
    } else {
      allClicked[selected.id] = "selected"
    }

    localStorage.setItem("selected", JSON.stringify(allClicked))
  }
  
  onMount(() => {
    const lSquare = localStorage.getItem("squares")!;
    const parsed = JSON.parse(lSquare)
    
    if (!parsed) {  // is not parsed
      console.log("not parsed")
      localStorage.setItem("squares", JSON.stringify(squares));
    } else {
      squares = parsed;
      const selected = localStorage.getItem("selected")!
      const ok = JSON.parse(selected)
      if (ok) {
        allClicked = ok
      }
      const themeType = localStorage.getItem("selectedTheme")!;
      selectedTheme = themeType as ThemeTypes;
    }
})

const changeBoardBasedOnTheme = () => {
 squares = setSquares();
 refreshBoard(true);
}

const changeThemeHandler = (e: any) => {
  if (e.target.nodeName === "DIV") {
    return;
  }

  selectedTheme = e.target.innerText;
  localStorage.setItem("selected", JSON.stringify({}));
  localStorage.setItem("selectedTheme", selectedTheme);
  changeBoardBasedOnTheme();
}

</script>

<main>
  <header class="header">
    <h1>Bingo!</h1>
    <p>Choose your board</p>
    <div on:click={changeThemeHandler}>
      {#each Themes as theme}
      <button class={`${theme.name === selectedTheme ? "selected-theme" : ""}`}>{theme.name}</button>
      {/each}
    </div>
    </header>
  <button on:click={() => {refreshBoard(true)}}> <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" fill="#000000" viewBox="0 0 256 256"><path d="M240,56v48a8,8,0,0,1-8,8H184a8,8,0,0,1,0-16H211.4L184.81,71.64l-.25-.24a80,80,0,1,0-1.67,114.78,8,8,0,0,1,11,11.63A95.44,95.44,0,0,1,128,224h-1.32A96,96,0,1,1,195.75,60L224,85.8V56a8,8,0,1,1,16,0Z"></path></svg></button>
  <div class="grid">
    {#each squares as square, index}
      <button class={`square ${allClicked[index]}`} on:click={onClick} id={"" + index}>
        <div>
          {square}
        </div>
      </button>
    {/each}
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
  max-width: 100%;
  /* width: calc(100vw - 4rem); */
 }

 .square {
  box-shadow: 0 0 0 2px black;
  overflow-wrap: break-word;
  word-wrap: break-word;
  word-break:break-all;
  /* word-break:; */
 }

 .selected {
  background-color: black !important;
  color: white !important;
 }

.selected-theme {
  background-color: orange;
}

.header {
  margin-bottom: 2.4rem;
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

 .square {
  padding: .6rem;
 }
</style>

<script setup lang="ts">
import { ref } from "vue";
import TeamBox from "./components/TeamBox.vue";

const tempname = ref("");
const names = ref([] as string[]);
const namesArr = ref<string[][]>([]);

// const nameTest = ref<string[]>(["adan", "eri"]);
const colors = ref([
  "purple",
  "pink",
  "orange",
  "white",
  "black",
  "green",
  "blue",
  "brown",
  "yellow",
] as string[]);

colors.value.sort(() => 0.5 - Math.random());

function pushNames(event: any) {
  if (event.key === "," && tempname.value) {
    const name = tempname.value.slice(0, -1);
    if (!names.value.includes(name)) {
      names.value.push(name);
    }

    tempname.value = "";
  }
}

function createTeams() {
  function shuffleNames() {
    const names2 = [...names.value];
    return names2.sort(() => 0.5 - Math.random());
  }
  const shuffledNames = shuffleNames();
  namesArr.value = [];

  let tempArr: string[] = [];
  for (let x of shuffledNames) {
    if (tempArr.length === 1 && namesArr.value.length === 8) {
      tempArr.push(x);
      namesArr.value.push(tempArr);
    } else if (tempArr.length < 2) {
      tempArr.push(x);
    } else {
      namesArr.value.push(tempArr);
      tempArr = [];
      tempArr.push(x);
    }
  }
}
</script>

<template>
  <div class="page entry home">
    <h1>Who's Playing?</h1>
    <input
      type="text"
      placeholder="Enter the name of all the participants separated by a comma."
      v-model="tempname"
      @keyup="pushNames"
    />
    <div class="nameslist">
      <span v-for="(nam, index) of names" :key="index"
        >{{ index + 1 }}. {{ nam }}</span
      >
    </div>

    <div class="teams">
      <div class="create-teams">
        <p>Click the button below to create teams</p>
        <button @click="createTeams">Create</button>
      </div>

      <TeamBox
        v-for="(color, index) in colors"
        :color="color"
        :key="index"
        :names="namesArr[index]"
      ></TeamBox>
    </div>
    <footer>
      <p>
        <span
          >© RandomTeams by
          <a href="https://adannaerica.com">Adanna Erica</a>.</span
        >
        From a builder to all the others.
      </p>
    </footer>
  </div>
</template>

<style scoped>
.page.entry.home {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  padding-top: 4rem;
}

h1 {
  font-size: 3rem;
  font-weight: bold;
}

input {
  border: none;
  border-bottom: 1px solid black;
  padding-bottom: 10px;
  font-family: "poppins";
}

input:focus-visible {
  outline: none;
}

input,
footer span {
  font-weight: 600;
  font-size: 12px;
}
.nameslist {
  display: flex;
  gap: 5px;
  flex-wrap: wrap;
}
.nameslist > span {
  font-size: 12px;
  font-weight: bold;

  background-color: black;
  padding: 5px 16px;
  border-radius: 20px;
  color: white;
}
.teams {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  justify-items: center;
  column-gap: 2rem;
  row-gap: 3.2rem;
  padding-bottom: 2rem;
}

.create-teams {
  width: 200px;
  height: 200px;
  border-radius: 1.4rem;
  border: 1px dashed black;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 1.4rem;
}

.create-teams > p {
  font-size: 12px;
  font-weight: 500;
  text-align: center;
  padding: 1.4rem 0;
}

.create-teams > button {
  color: black;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-size: 12px;
  font-weight: bold;
  font-family: "poppins";
  width: 100%;
  padding: 0.6rem;
  border-radius: 8px;
  border: none;
  background-color: #efefef;
  transition: all 0.5s ease-in-out;
}

.create-teams > button:hover {
  background-color: rgb(203, 202, 202);
}
</style>

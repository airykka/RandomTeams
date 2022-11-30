<template>
  <div class="teambox" :class="color">
    <div class="color-palette"></div>
    <div class="team-heading">
      Team {{ color[0].toUpperCase() + color.slice(1).toLowerCase() }}
    </div>
    <div class="team-members">
      <p v-for="name of names" class="team-member" :key="name">{{ name }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
// export type Props = {
//   color: string;
//   names: string[];
// };

withDefaults(
  defineProps<{
    color: string;
    names: string[];
  }>(),
  {
    names: () => ["-", "-"],
  }
);
</script>

<style scoped>
.teambox {
  width: 200px;
  height: 200px;
  border-radius: 1.4rem;
  background-color: rgb(181, 181, 234);
  display: flex;
  gap: 1rem;
  flex-direction: column;
  align-items: center;
}

.teambox.pink {
  background-color: var(--tb-pink-soft);
  border: 1px solid var(--tb-pink);
}

.teambox.pink > .color-palette {
  background-color: var(--tb-pink);
}
.teambox.purple {
  background-color: var(--tb-purple-soft);
  border: 1px solid var(--tb-purple);
}

.teambox.purple > .color-palette {
  background-color: var(--tb-purple);
}
.teambox.orange {
  background-color: var(--tb-orange-soft);
  border: 1px solid var(--tb-orange);
}

.teambox.orange > .color-palette {
  background-color: var(--tb-orange);
}
.teambox.brown {
  background-color: var(--tb-brown-soft);
  border: 1px solid var(--tb-brown);
}

.teambox.brown > .color-palette {
  background-color: var(--tb-brown);
}
.teambox.black {
  background-color: var(--tb-black-soft);
  border: 1px solid var(--tb-black);
}

.teambox.black > .color-palette {
  background-color: var(--tb-black);
}
.teambox.blue {
  background-color: var(--tb-blue-soft);
  border: 1px solid var(--tb-blue);
}

.teambox.blue > .color-palette {
  background-color: var(--tb-blue);
}
.teambox.green {
  background-color: var(--tb-green-soft);
  border: 1px solid var(--tb-green);
}

.teambox.green > .color-palette {
  background-color: var(--tb-green);
}
.teambox.yellow {
  background-color: var(--tb-yellow-soft);
  border: 1px solid var(--tb-yellow);
}

.teambox.yellow > .color-palette {
  background-color: var(--tb-yellow);
}
.teambox.white,
.teambox.white > .color-palette {
  background-color: var(--tb-white);
  border: 1px solid var(--tb-black);
}

.color-palette {
  margin-top: 14px;
  width: 90%;
  background-color: antiquewhite;
  height: 25%;
  border-radius: 12px;
}

.team-heading,
.team-member {
  color: black;
  text-align: center;
}

.team-heading {
  font-weight: bold;
  font-size: 16px;
}

.team-member {
  font-weight: 500;
  font-size: 14px;
}
</style>

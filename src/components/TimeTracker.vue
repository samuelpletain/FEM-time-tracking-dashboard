<script setup>
import {ref, onMounted} from 'vue'
import Card from './Card.vue';

const data = ref(undefined)
const amount = ref("weekly")

async function fetchData() {
  const response = await fetch('data.json').then((r) => r.json())
  data.value = response
  for (const item in data.value) {
    data.value[item].image = data.value[item].title.toLowerCase().replace(' ', '-')
  }
}

onMounted(() => {
  fetchData()
})

</script>

<template>
  <div class="tracker">
    <div class="tracker__user-pannel user-pannel">
      <div class="user-pannel__user-info user-info">
        <img src="@/assets/image-jeremy.png" alt="Portrait of Jeremy Robson" class="user-info__avatar">      
        <h1 class="user-info__title">
          Report for
          <span class="user-info__title--large">
            Jeremy Robson
          </span>
        </h1>
      </div>
      <ul class="user-pannel__time-pannel time-pannel">
        <li class="time-pannel__time-span" @click="amount = 'daily'" :class="amount == 'daily'? 'active': ''">Daily</li>
        <li class="time-pannel__time-span" @click="amount = 'weekly'" :class="amount == 'weekly'? 'active': ''">Weekly</li>
        <li class="time-pannel__time-span" @click="amount = 'monthly'" :class="amount == 'monthly'? 'active': ''">Monthly</li>
      </ul>
    </div>
    <Card v-for="item in data" :title="item.title" :current-hours="item.timeframes[amount].current" :past-hours="item.timeframes[amount].previous" :image="item.image" :key="item.title" :class="item.image"></Card>
  </div>
</template>

<style lang="scss" scoped>
.tracker {
  z-index: -4;
  padding: 1em;
  background-color: $neutral-900;
  display: grid;
  gap: 1rem;
  max-width: 1000px;
  margin: auto;
  grid-template-areas: 
    'one'
    'two'
    'three'
    'four'
    'five'
    'six'
    'seven';
    grid-auto-columns: 1fr;
    @include breakpoint {
      grid-template-areas: 
        'one two three four'
        'one five six seven';
    }
    gap: 1.5rem;
}

.user-pannel {
  border-radius: 10px;
  background-color: hsl(235, 46%, 20%);
  grid-area: one;
  z-index: 1;
}

.user-info {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-evenly;
  background-color: $primary;
  padding: 1.5em 1em;
  border-radius: 10px;
  @include breakpoint {
    height: 70%;
    flex-wrap: nowrap;
    align-content: flex-start;
    flex-direction: column;
    justify-content: normal;
    align-items: flex-start;
    gap: 2em;
  }
  &__avatar {
    width: 20%;
    border-radius: 50%;
    border: 3px solid #fff;
    @include breakpoint {
      height: 4em; 
      width: 4em;
    }
  }
  &__title {
    color: hsl(236, 100%, 87%);
    font-weight: 400;
    font-size: .8em;
    &--large {
      display: block;
      color: #fff;
      font-size: 1.8em;
      font-weight: 300;
      @include breakpoint {
        font-size: 2.5em;
      }
    }
  }
}

.time-pannel {
  list-style: none;
  display: flex;
  justify-content: space-between;
  padding: 1.5em 2em;
  color:hsl(235, 45%, 61%);
  flex-wrap: wrap;
  @include breakpoint {
    padding: 1em 1.5em;
    flex-direction: column;
    gap: .5em;
    height: 30%;
    flex-wrap: nowrap;
  }
  &__time-span:hover {
    color: #fff;
    cursor: pointer;
  }
}

.active {
  color: #fff;
}

.work::before {
  grid-area: two;
  background-color: hsl(15, 100%, 70%);
  background-image: url('@/assets/icon-work.svg');
}

.play::before {
  grid-area: three;
  background-color: hsl(195, 74%, 62%);  
  background-image: url('@/assets/icon-play.svg');
  background-position-y: -6px;
}

.study::before {
  grid-area: four;
  background-color: hsl(348, 100%, 68%);  
  background-image: url('@/assets/icon-study.svg');
  background-position-y: -8px;
}

.exercise::before {
  grid-area: five;
  background-color: hsl(145, 58%, 55%);  
  background-image: url('@/assets/icon-exercise.svg');
  background-position-y: -2px;
}

.social::before {
  grid-area: six;
  background-color: hsl(264, 64%, 52%);
  background-image: url('@/assets/icon-social.svg');  
  background-position-y: -16px;
}

.self-care::before {
  grid-area: seven;
  background-color: hsl(43, 84%, 65%);  
  background-image: url('@/assets/icon-self-care.svg');  
  background-position-y: -12px;
}

.self-care>img {
  top: -12px;
}
</style>
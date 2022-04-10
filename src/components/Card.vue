<script setup>
  import { ref, computed, onMounted } from 'vue'

  defineProps({
    title: String,
    image: String,
    currentHours: Number,
    pastHours: Number
  })
</script>

<template>
  <div class="wrap">
    <div class="dots">
      <img src="@/assets/icon-ellipsis.svg" alt="Ellipsis icon">
    </div>
    <div class="card">
      <h2 class="card__title">{{ title }}</h2>
      <p class="card__currentHours">{{ currentHours }}hrs</p>
      <p class="card__pastHours">Last Week - {{ pastHours }}hrs</p>
    </div>
  </div>
</template>

<style lang="scss" scoped>

.wrap {
  position: relative;
  &::before {
    content: '';
    height: 3rem;
    width: 100%;
    display: block;
    z-index: -1;
    position: absolute;
    background-color: white;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;    
    background-origin: content-box;     
    background: $neutral-400 no-repeat calc(100% - 1rem);
  }
}

.card {
  color: #fff;
  position: relative;
  border-radius: 10px;
  background-color: $neutral-700;
  padding: 1.5rem;
  display: flex;  
  justify-content: space-between;
  flex-wrap: wrap;
  align-items: center;
  margin-top: calc(3rem - 12px);
  @include breakpoint {
    min-height: calc(200px - 3rem);
  }
  &:hover {
    background-color: lighten($neutral-700, 10);
    cursor: pointer;
  }
  &__title {
    z-index: 1;
    width: 90%;
    font-weight: 500;
    margin-bottom: .5rem;
    position: relative;
    font-size: 18px;
    @include breakpoint {
      width: 80%;
    }
  }
  &__currentHours {
    z-index: 1;
    font-size: 2rem;
    font-weight: 300;
    @include breakpoint {
      font-size: 3em;
      width: 100%;
    }
  }
  &__pastHours {
    z-index: 1;
    font-size: .8rem;
    font-weight: 400;
    text-align: right;
    color: $neutral-400;
    @include breakpoint {
      text-align: left;
    }
  }
}

.dots {
  position: absolute;
  top: 3.5rem;
  z-index: 3;
  right: 1.5rem;
  &:hover {
    cursor: pointer;
    filter: brightness(0) saturate(100%) invert(100%);
    & + .wrap  {
      background-color: $neutral-100;
    }
  }
}
</style>
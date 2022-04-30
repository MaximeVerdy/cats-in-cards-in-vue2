<template>
  <div class="card">
    <img :src="img" class="card__img" />
    <div class="card__body">
      <h2 class="card__title">{{ title }}</h2>
      <p class="card__description">{{ coat }} coat</p>
      <p class="card__description">{{ pattern }} pattern</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "CatCard",
  props: {
    title: String,
    coat: String,
    pattern: String,
    img: String,
  },
};
</script>
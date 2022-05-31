<template>
  <div class="child">
    <div class="childMainVisual">
      <div class="container container--lg">
        <h1 class="childMainVisual__title">Works</h1>
        <p>成果物をご紹介します。</p>
      </div>
    </div>

    <div class="container">
      <WorksList :works="works" />
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $microcms }) {
    const works = await $microcms.get({
      endpoint: 'blog',
    })
    return {
      works,
    }
  },
}
</script>

<style lang="scss" scoped>
.childMainVisual {
  text-align: center;
  padding: 5em 0;
  background-color: $base-color-secondary;
  margin-bottom: 2.5em;

  @include mq() {
    margin-bottom: 5em;
  }

  &__title {
    font-family: $font-ubuntu;
    font-size: fz(40);
    margin-bottom: 0.25em;
  }
}

.works {
  list-style: none;

  &__item {
    width: 100%;

    @include mq() {
      width: calc((100% - 2.5em) / 2);
    }
  }

  &__item + &__item {
    margin-top: 1.5em;

    @include mq() {
      margin: 0;
    }
  }

  &__inner {
    display: block;
  }

  &__image {
    margin-bottom: 0.5em;

    img {
      width: 100%;
    }
  }

  &__name {
    font-weight: bold;
  }

  &__date {
    font-size: fz(14);
  }
}
</style>

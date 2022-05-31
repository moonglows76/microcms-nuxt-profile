<template>
  <ol class="row works">
    <li v-for="work in works.contents" :key="work.id" class="works__item">
      <nuxt-link :to="`/works/${work.id}/`" class="works__inner">
        <figure class="works__image">
          <img
            :width="work.thumbnail.width"
            :height="work.thumbnail.height"
            :src="work.thumbnail.url"
            :alt="work.title"
          />
        </figure>
        <div class="works__text">
          <p class="works__name">{{ work.title }}</p>
          <p class="works__date">
            <time
              :datetime="work.release"
              v-text="$dateFns.format(new Date(work.release), 'yyyy.MM.dd')"
            />
          </p>
        </div>
      </nuxt-link>
    </li>
  </ol>
</template>

<script>
export default {
  props: {
    works: {
      type: Object,
      default: () => {}
    }
  },
}
</script>

<style lang="scss" scoped>
.works {
  list-style: none;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;

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

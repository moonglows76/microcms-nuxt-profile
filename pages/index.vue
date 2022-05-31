<template>
  <div>
    <div class="mainVisual">
      <picture>
        <source
          :width="settings.mainVisualSp.width"
          :height="settings.mainVisualSp.height"
          :srcset="settings.mainVisualSp.url"
          media="(max-width: 767px)"
        />
        <img
          :width="settings.mainVisualPc.width"
          :height="settings.mainVisualPc.height"
          :src="settings.mainVisualPc.url"
          alt=""
        />
      </picture>
    </div>

    <section id="about" class="sectionPrimary">
      <div class="container">
        <h2 class="headingPrimary">about</h2>
        <div class="profile">
          <div class="profile__upper">
            <div class="profile__text">
              <p class="profile__name">
                <span>{{ settings.name }}</span>
                <span lang="en">{{ settings.nameEnglish }}</span>
              </p>
              <dl class="profile__item">
                <dt class="profile__title">技術スタック</dt>
                <dd>{{ settings.skills }}</dd>
              </dl>
              <dl class="profile__item">
                <dt class="profile__title">趣味</dt>
                <dd>{{ settings.hobby }}</dd>
              </dl>
            </div>
            <figure class="profile__image">
              <img
                :width="settings.profileImage.width"
                :height="settings.profileImage.height"
                :src="settings.profileImage.url"
                :alt="settings.name"
              />
            </figure>
          </div>
          <p class="profile__message">{{ settings.message }}</p>
        </div>
      </div>
    </section>

    <section class="sectionPrimary background--gray">
      <div class="container">
        <h2 class="headingPrimary">works</h2>
        <WorksList :works="works" />
        <p class="button-area">
          <nuxt-link to="/works" class="buttonPrimary">view more</nuxt-link>
        </p>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  async asyncData({ $microcms }) {
    const settings = await $microcms.get({
      endpoint: 'settings',
    })
    const works = await $microcms.get({
      endpoint: 'blog',
      queries: { limit: 2 },
    })
    return {
      settings,
      works,
    }
  },
}
</script>


<style lang="scss" scoped>
.mainVisual {
  img {
    width: 100%;
  }
}

.profile {
  &__upper {
    display: flex;
    flex-direction: column-reverse;
    margin-bottom: 0.5em;

    @include mq() {
      flex-direction: row-reverse;
      justify-content: space-between;
      margin-bottom: 2em;
    }
  }

  &__text {
    @include mq() {
    }
  }

  &__name {
    font-size: fz(24);
    font-weight: bold;
    margin-bottom: 0.5em;

    @include mq() {
      font-size: fz(28);
      margin-bottom: 0.857em;
    }

    [lang='en'] {
      font-size: fz(18);

      &::before {
        content: '/';
        margin: 0 0.5em;
      }
    }
  }

  &__item {
    margin-bottom: 0.5em;

    @include mq() {
      margin-bottom: 1em;
    }
  }

  &__title {
    font-size: fz(18);
    font-weight: bold;
    margin-bottom: 0.222em;

    @include mq() {
      margin-bottom: 0.444em;
    }
  }

  &__image {
    width: 100%;
    margin-bottom: 1.75em;

    @include mq() {
      width: 40%;
      margin: 0 2em 0 0;
    }

    img {
      width: 100%;
    }
  }

  &__message {
    white-space: pre-wrap;
  }
}
</style>

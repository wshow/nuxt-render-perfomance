<template>
  <div>
    <template v-if="$fetchState.pending">
      Loading
    </template>
    <template v-else-if="$fetchState.error">
      Error
    </template>
    <template v-else>
      <h1>{{ title }}</h1>
      <div v-html="html"></div>
    </template>
  </div>
</template>

<script>
export default {
  async fetch() {
    const { title, html } = await import(`~/assets/posts/${this.slug}.json`);
    this.title = title;
    this.html = html;
  },
  data() {
    return {
      slug: this.$route.params.slug,
      title: '',
      html: ''
    };
  }
};
</script>

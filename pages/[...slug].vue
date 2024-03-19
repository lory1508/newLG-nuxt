<template>
  <Menu />
  <Header
    :title="hero.title"
    :subtitle="hero.subtitle"
    :image="hero.image"
    :gradient="hero.gradient"
  />
</template>

<script setup lang="ts">
import Menu from "~/components/Menu.vue";
import Header from "~/components/Header.vue";
import { ref, onMounted } from "vue";

const route = useRoute();
const slug = ref("");

const hero = ref({
  title: "",
  subtitle: "",
  content: "",
  image: "",
  gradient: {
    from: "",
    to: "",
  },
});

if (route.params.slug) {
  let lastIndex = route.params.slug.length - 1;

  if (route.params.slug[lastIndex] === "/") {
    slug.value = route.params.slug[lastIndex - 1];
  } else {
    slug.value = route.params.slug[lastIndex];
  }
} else {
  slug.value = "home";
}

const { data, pending, error, refresh } = useFetch(
  "https://lorenzogalassi.com/wp-json/wp/v2/pages",
  {
    query: { slug: slug.value },
  }
);

onMounted(async () => {
  console.log(data.value[0]);

  if (data.value[0].acf) {
    hero.value = {
      title: data.value[0].acf.header.title,
      subtitle: data.value[0].acf.header.subtitle,
      content: data.value[0].content.rendered,
      image: data.value[0].acf.header.hero_image,
      gradient: {
        from: data.value[0].acf.header.gradient_from,
        to: data.value[0].acf.header.gradient_to,
      },
    };
  }
  console.log(hero.value);
});
</script>

<style scoped></style>

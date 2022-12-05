<template>
  <div>
    <Head>
      <Title>Nuxt Dojo | {{ product.title }}</Title>
      <Meta name="description" :content="product.description" />
    </Head>
    <ProductDetail :product="product" />
  </div>
</template>

<script setup>
definePageMeta({
  layout: "products",
});

const { id } = useRoute().params;
const uri = "https://fakestoreapi.com/products/" + id;

// fetch the product

const { data: product } = await useFetch(uri, { key: id });

if (!product.value) {
  throw createError({
    status: 404,
    statusMessage: "Product Not Found!",
    fatal: true,
  });
}
</script>

<style scoped></style>

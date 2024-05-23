<template>
    <q-card class="q-mb-md">
      <q-card-section>
        <div class="text-h6">{{ product.name }}</div>
      </q-card-section>
      <q-img :src="product.image" ratio="16:9" />
      <q-card-section>
        <p>{{ product.description }}</p>
        <q-btn color="primary" label="Buy Now" />
      </q-card-section>
    </q-card>
  </template>
  
  <script>
  export default {
    name: 'ProductCard',
    props: {
      product: {
        type: Object,
        required: true
      }
    }
  };
  </script>
  
<template>
  <q-layout view="lHh lpr lFf">
    <q-header elevated class="header">
      <q-toolbar>
        <q-toolbar-title>Gitarkuu</q-toolbar-title>
        <q-space />
        <q-input v-model="search" debounce="300" placeholder="Cari Gitar..." @input="filterProduk" outlined dense></q-input>
        <q-btn flat round dense icon="shopping_cart" @click="goToCartPage" class="header-btn" />
        <q-btn flat round dense icon="person" @click="goToProfilePage" class="header-btn" />
      </q-toolbar>
    </q-header>

    <q-page-container>
      <q-page padding class="page-background">
        <q-carousel
          animated
          v-model="slide"
          :autoplay="5000"
          arrows
          infinite
          class="carousel"
        >
          <q-carousel-slide
            :name="1"
            img-src="data:image/jpeg;base64,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"
          />
          <q-carousel-slide
            :name="3"
            img-src="data:image/jpeg;base64,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"
          />
          <q-carousel-slide
            :name="4"
            img-src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRa7lh52jDXkWzPYjboRicH4GpJch2HmzUy7HPx6DnYTZ3wS1rrXNTKKV4LvcZI6jQsxnM&usqp=CAU"
          />
        </q-carousel>

        <q-tabs v-model="tab" class="q-mt-lg tabs" align="justify" indicator-color="primary">
          <q-tab name="semua" label="Semua" />
          <q-tab name="Akustik" label="Akustik" />
          <q-tab name="Elektrik" label="Elektrik" />
        </q-tabs>

        <q-tab-panels v-model="tab" animated>
          <q-tab-panel name="semua" class="tab-panel">
            <div class="q-gutter-md">
              <q-card
                v-for="produk in filteredProduk"
                :key="produk.nama"
                class="q-ma-md produk-card"
              >
                <q-card-section>
                  <q-img
                    :src="produk.gambar"
                    class="product-image"
                    :alt="produk.nama"
                  />
                  <div class="product-details">
                    <div class="text-h6">{{ produk.nama }}</div>
                    <div class="text-subtitle2">Kategori: {{ produk.kategori }}</div>
                    <div class="text-subtitle2">Harga: Rp {{ produk.harga }}</div>
                    <q-rating v-model="produk.rating" max="5" size="20px" color="amber" />
                    <q-btn color="primary" label="Tambah ke Keranjang" @click="addToCart(produk)" class="add-to-cart-btn"></q-btn>
                  </div>
                </q-card-section>
              </q-card>
            </div>
          </q-tab-panel>

          <q-tab-panel name="boneka" class="tab-panel">
            <div class="q-gutter-md">
              <q-card
                v-for="produk in filteredProduk"
                :key="produk.nama"
                class="q-ma-md produk-card"
              >
                <q-card-section>
                  <q-img
                    :src="produk.gambar"
                    class="product-image"
                    :alt="produk.nama"
                  />
                  <div class="product-details">
                    <div class="text-h6">{{ produk.nama }}</div>
                    <div class="text-subtitle2">Kategori: {{ produk.kategori }}</div>
                    <div class="text-subtitle2">Harga: Rp {{ produk.harga }}</div>
                    <q-rating v-model="produk.rating" max="5" size="20px" color="amber" />
                    <q-btn color="primary" label="Tambah ke Keranjang" @click="addToCart(produk)" class="add-to-cart-btn"></q-btn>
                  </div>
                </q-card-section>
              </q-card>
            </div>
          </q-tab-panel>

          <q-tab-panel name="kendaraan" class="tab-panel">
            <div class="q-gutter-md">
              <q-card
                v-for="produk in filteredProduk"
                :key="produk.nama"
                class="q-ma-md produk-card"
              >
                <q-card-section>
                  <q-img
                    :src="produk.gambar"
                    class="product-image"
                    :alt="produk.nama"
                  />
                  <div class="product-details">
                    <div class="text-h6">{{ produk.nama }}</div>
                    <div class="text-subtitle2">Kategori: {{ produk.kategori }}</div>
                    <div class="text-subtitle2">Harga: Rp {{ produk.harga }}</div>
                    <q-rating v-model="produk.rating" max="5" size="20px" color="amber" />
                    <q-btn color="primary" label="Tambah ke Keranjang" @click="addToCart(produk)" class="add-to-cart-btn"></q-btn>
                  </div>
                </q-card-section>
              </q-card>
            </div>
          </q-tab-panel>
        </q-tab-panels>

        <div class="q-my-lg">
          <q-banner class="q-mb-lg promo-banner" color="purple-5" text-color="white" inline-actions>
            <div class="text-h6">Promo Hari Ini!</div>
            <div>Diskon 20% untuk semua mainan edukatif.</div>
            <q-btn flat label="Lihat Promo" text-color="white" @click="lihatPromo" />
          </q-banner>
        </div>

        <div class="q-my-lg">
          <q-card class="q-ma-md testimoni-card">
            <q-card-section class="testimoni-section">
              <q-avatar icon="person" />
              <div class="testimoni-details">
                <div class="text-subtitle1">Riski</div>
                <div class="q-mt-sm">"Gitar di toko ini sangat bagus dan saya sangat suka!"</div>
              </div>
            </q-card-section>
          </q-card>
          <q-card class="q-ma-md testimoni-card">
            <q-card-section class="testimoni-section">
              <q-avatar icon="person" />
              <div class="testimoni-details">
                <div class="text-subtitle1">Aqsheina</div>
                <div class="q-mt-sm">"Pelayanan cepat dan Gitarnya berkualitas. Sangat puas beli di sini!"</div>
              </div>
            </q-card-section>
          </q-card>
        </div>

      </q-page>
    </q-page-container>

    <q-footer elevated class="footer">
      <q-toolbar>
        <q-toolbar-title>
          @toko_gitar
        </q-toolbar-title>
        <q-space />
        <q-btn flat round dense icon="phone" @click="contactUs" />
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script>
import { ref, watch } from "vue";

export default {
  setup() {
    const slide = ref(1);
    const tab = ref('semua');
    const search = ref('');
    const produk = ref([
  {
    nama: "Gitar Klasik",
    kategori: "akustik",
    harga: 10000000,
    gambar: "data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkGBw8QEg8REBIQDxURERUQEg8SFRASEA8PFRcWFhUWExMYKCggGBolGxUWITEhJSkrLy4xFx81ODktNygtLi0BCgoKDg0OGxAQGy0lHh0vLS0rLS0vLS0tLS8tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLf/AABEIAOEA4QMBEQACEQEDEQH/xAAcAAEAAQUBAQAAAAAAAAAAAAAABQIDBAYHAQj/xAA+EAACAQIDAwcJBgUFAAAAAAAAAQIDEQQSIQUxQQYHEyJRYXEUIzJCgZGhsdEkM1JiwfAWQ1RykxVTktLh/8QAGQEBAAMBAQAAAAAAAAAAAAAAAAECBAUD/8QAMBEBAAICAAQDBgYCAwAAAAAAAAECAxEEEiExE0FRFGFxgZGxIjIzUsHwQvEFI6H/2gAMAwEAAhEDEQA/AO4gAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABxHnD5U4zy3E0aWKqxoU5U1CNGSpq7pwclnhZy6zlvbRz+Iy2i/Lvo7HC4cfgxfUTM77/H6Ne2ftvG0ZZ6WJxFNKWl6knFuT1vCTal7UZ7cRaPyS0VwUt+pWOv98nfeTWLlWwmFqTl0k50abqTtFZqjiszaVktb6JHVx2m1ImfOHEzViuS1Y7RMpIu8gAAAAAAAAAAAAAAAAAAAAAAAAAAAADh/JfZWGr0tt3jCLpRzUnUVNzi30z6uXqp3gvR7TDNIte+/70dKLzXHi16z91vkdsmjisNtOdVQvRoxcJTTbjJRqSvDVWfVWuu88OGxRNbbauMyTW9Ij1dB5p6dNYFumms1epKd4wjmqdVNq2slZLV6+yxv4f8ASr8Icrip/wC63xn7tzPZ4AAAAAAAAAAAAAAAAAAAAAAAAAAAAAHHeSFSnCttqGIhmlJRahCG5x6dSllu7WvF734maNc9tw3334GPXrP8KeRkqUNn7Vzwc2lOPo3yvossW3w6z+ZmwzFcVtx221cVu2fHrz1928c2EJrAQU1FecnlcY5c0L6N6vM96vpu3du3B+nX4OZxH6tvjP3bYerxAAAAAAAAAAAAAAAAAAAAAAAAAAAAAObc5XJzB0Yxxt6lKbrRpzlFZ1NTzJJwutb5db6JHjfFE9Y7tOLiJrHLPWGk8l8LgsRjaGHdWtJV5typ9G6cZpKc7OSk7awZnjhJ5tzPRrt/yEcuq16+U+jvODwsKMI04aRgssV2RW5exG2I1Gocy0zM7leJQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAaNzxW8gje6XleH3JN+npoRKYcx5BKnHaezmpTvdpJxik7qst9+98BPZL6HJVAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAGic8k0sDRulK+Nw6s729JvhZ8CJTDmXI2pH/AFDZfUgr1Erp1Lq7rrS8re/tE9kvoglUAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAaLzv5vJMPl0fllHilp1r7+4iVqua8l3VWN2W21bpqd+tT4zqLtu963DppL6EJUAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAGhc8TXkmHUm1fF0ndJN3V+F12kT3TDl/J9QWL2W1Kd1iKNuol/Nlv62nxHXSX0aSqAAAAAAAAAAAAAAAAAAAAAAAAAAAAAANB54L+T4ZJRf2mGksrVk1+LiRPdarmWxJT8p2e2qStWovdRuvOPd7xPZL6LJUAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAHPeeNroMLdN/aIvRpa3iux9pE91ocp2VWp9Pg3aelSj68f8Adp71l7xPZL6YJUAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAHO+eOplpYTrSh53fHe+tT03oie61XJ8DjLVKD6at6dJWtv69B69fv+ImOiX04SoAAAAAAAAAAAAAAAAAAAAAAAAAAAAAWp4iC4+7U8rZqV814x2lzbnjxqyYNKU4edavFJ3u4tLevwMrTLF7dPJaaTWOrlFPGJSp2rVV1qfqrXXD/n7/AIntMdFX07HGw7WvFP8AQ8I4nHK04bQvxknqmn4HvExMbh5zEx3ekoAAAAAAAAAAAAAAAAAAAAAAAAABg4iu3dLd8zFlyzbpHZox011lhyZjmWiGgc6c5fZVHpPvI36N5Xa0vS7v/DVwk7mfk8s3aPn/AA5pmq3hbyv1H947fyH2fvU3eTO+hHPd4I4kz2dCIXqFZp3Wn6+J7Ysk1ncPO9ImOqWo1cyv712M6eO8XjbFavLOlwuqAAAAAAAAAAAAAAAAAAAAAAALeIlaMvA88s6pMrUjdoRbZzZls0oZSV4c552LOWDTyPzqazdI9cs92Tjrx0NXB97fL+Xjn7R83LcQoJXth9IQeqxv4aD4fv4m9mfSC3R8EcGXShVAtBKRwE+tbtRu4a34terJmjokDczAAAAAAAAAAAAAAAAAAAAAAACitG8ZLuKZI5qzC1Z1MSh2zlNy1iK8acZTm8sYRcpPsildsiImZ1CZ6RtybnD2jVq1aKTcJU6kXOnG6VKMoycYSkvTnpeXBNpK9mzdw9OXc+rPktvo51isTiFFrpJ/dx3TqLXJQb/U0xLy1LvvJnbscTCPWjLNFzpTXVc4RajUjOHqzhJqL4O8Wt9lx82Pln+/3q247b6J48nokdmK7b7F8/2zocJG52ycRPTSSN7KAAAAAAAAAAAAAAAAAAAAAAAAEPiY2lJd/wA9TlZq8t5huxzusSjNsPzcdbJ16Cl/Y60E14Pd7StO/wBfsm8bhoO2dm3c3JNylUzSdvWvK/zOtERqNMcz1aBjtnNTs1LWPZw6OH0Gk7blzb0pwcUrqLx0nbtUsLW6Re+NF+xGLi9Rv4fz/towRv5T/DqEZHNhqmE1syFoX7W/hp9TrcJXWPfqwcRO769GYangAAAAAAAAAAAAAAAAAAAAAAAAENjKl5yt4e7Q5Ge+8k6b8VdUhiYmjGpCUJbpJp23q/Fd55RbU7Xmu401TbSqWtKMM+ZJuclTpV9HaVOb6qk+MG0072urHRxcR+HXeP8A2Ge+LctNlsXFVKkXUp0MNG1s0q1KctYx9CnTzSm7tqyWtj0niI8omVYxe9v2wtkxoKLUXFRUowjL025tOpUmuEpZYpLgopcWc3Pl5p/v0asWOIhNU2eFe71lPbNmnC34W179f1Oxw1ommvRzs8atv1ZZoeIAAAAAAAAAAAAAAAAAAAAAAAxsdiMke96L6nhxGXw6++Xrix89vchbnHdDT1SESjSzNp3vqr7i0SmYW6VGnHWMIRvvcYxV/cJtM95IrEK58SkphSmISzcDiXCV+D0a7jRhyzS2/LzeGXHzVTqd9UdeJ31c96SAAAAAAAAAAAAAAAAAAAAAPGwIHGV88m+G5eBxs+Tntt0cVOWulhs8Xo8zEJWpv5k+Q8zbv3xA9chI8Q0LtItWFZTWza2mR8NV4HR4XJ/hPyY89P8AKGcbGcAAAAAAAAAAAAAAAAAAAABibUq5YP8AM8vs4mbir8uP4vbBXd/ggmzky3wpnNLV6W1b7EE6RD5T7PW/F4X/ADUvqXjDk/bP0RzV9Vj+KMA92Kwr1t99S3rXtJ8K/wC2foc9fVbnyr2erXxeFWietalueq49jJ8HJ+2fojxKesH8W7O/rMJ/mpfUeDk/bJ4lPWGZs7lBg68+joYihWnZyyQqQlKy3uy4CcVqxuYRz1ntKZgQMvDzs4vsPWk6mJed43EwnEzrMAAAAAAAAAAAAAAAAAAAAACK24/u14v5GDjp/L82rhfNEtnPbFjGRcoVEtW4SSXe0yI7j57jyB2t/ST/AOVH/sdn2rF+5zvAv6J3Zmztt0qdOnlxEFB1up0iWWEaS6KMbStZzcvdw4z4+P1PCv6KsTg9uv0fK+zSrK2lKKvv166bI9oxeqfByeiKx3JnbmJy9NSxFbKll6SrTeVtLNbNLS7S9w9pxR5ngZJ8mxc2XJPaGExqrYig6UOiqQcnOlLrStZWi2+Bn4jPjvTVZeuHFettzDrykYNtWmTRkXrKloT+Hd4x8EdfFO6Q59/zSuHoqAAAAAAAAAAAAAAAAAAABFbdjpTfe177fQwcdHSstXDT1mEPJnOlshSyEqQl62Sh4wKGgCAuRZKGRRZaqstkw8bRivyo7WONUiHNvO7TK4XVAAAAAAAAAAAAAAAAAAAAx8dh+kg48d68UeWbH4lJhfHflttrFTS6ejWjXYziTGp6unE7U3ISAEB60SKZRJQ8URo2riShJbLw+eXdHV/Q08Pi57e6Hhmvyx8U8dVhAAAAAAAAAAAAAAAAAAAAAAI7aezVU60bKXwl49/eZOI4XxPxV7/dow5uTpPZr9enKm7Ti4+O5+D4nLvS1J1aNN1bRaOkrakVSrTJFVyUPHIlDxtAZuC2fUqNaOMfxP8ARcT2xcPe/uh5Xy1r8Ww4ejGEVGO74t9rOrjpFK6hhtabTuVwuqAAAAAAAAAAAAAAAAAAAAAAAPJRTVmk12PVETET0lMTphz2VQfqJf23j8EeFuFxT5PSM+SPNbexqP5l7SnsWP3re03W6ew6acs0pST3LRZV4rePYsfvT7TdejsigvVb8ZSLRwmL0VnPf1ZNLCU4ejCK77K/vPWuKle0POb2nvK8eioAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAf/9k=",
    rating: 4.5
  },
  {
    nama: "Gitar Bass",
    kategori: "elektrik",
    harga: 800000,
    gambar: "data:image/jpeg;base64,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",
    rating: 4.7
  },
  {
    nama: "Gitar Hollowbody",
    kategori: "akustik",
    harga: 1500000,
    gambar: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRwZCx1LhYpuHsdYUzdINB91WnDQ0LgrLMAtw&usqp=CAU",
    rating: 4.8
  },
  {
    nama: "Gitar RGX121Z",
    kategori: "elektrik",
    harga: 2000000,
    gambar: "data:image/jpeg;base64,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",
    rating: 4.9
  },
]);

    const filteredProduk = ref(produk.value);

    watch(search, (newVal) => {
      filteredProduk.value = produk.value.filter((item) => 
        item.nama.toLowerCase().includes(newVal.toLowerCase())
      );
    });

    const filterProduk = () => {
      filteredProduk.value = produk.value.filter((item) => 
        item.kategori === tab.value || tab.value === 'semua'
      );
    };

    watch(tab, filterProduk);

    const addToCart = (item) => {
      console.log('Produk ditambahkan ke keranjang:', item);
    };

    const goToCartPage = () => {
      console.log('Menuju halaman keranjang');
    };

    const goToProfilePage = () => {
      console.log('Menuju halaman profil');
    };

    const lihatPromo = () => {
      console.log('Melihat promo');
    };

    const contactUs = () => {
      console.log('Menghubungi kami');
    };

    return {
      slide,
      tab,
      search,
      produk,
      filteredProduk,
      filterProduk,
      addToCart,
      goToCartPage,
      goToProfilePage,
      lihatPromo,
      contactUs
    };
  },
};
</script>

<style scoped>
.header {
  background-color: #ec913c;
  color: white;
}
.header-btn {
  margin-left: 8px;
}
.page-background {
  background: white;
}
.carousel {
  height: 300px;
}
.tabs {
  background-color: #ec913c;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
.tab-panel {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.produk-card {
  width: 300px;
}
.product-image {
  height: 200px;
  object-fit: cover;
}
.product-details {
  text-align: center;
}
.add-to-cart-btn {
  margin-top: 10px;
}
.promo-banner {
  padding: 16px;
}
.testimoni-card {
  max-width: 600px;
  margin: 16px auto;
}
.testimoni-section {
  display: flex;
  align-items: center;
}
.testimoni-details {
  margin-left: 16px;
}
.footer {
  background-color: #ec913c;
  color: white;
}  
</style>
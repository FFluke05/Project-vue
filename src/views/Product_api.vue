<template>
  <div class="container my-5 pb-5">
    <h2 class="text-center fw-bold text-gradient title-3d mb-5">
      สินค้าทั้งหมด
    </h2>

    <div class="row g-4">
      <div
        class="col-md-4 col-lg-3"
        v-for="product in products"
        :key="product.id"
      >
        <div class="card-3d h-100 d-flex flex-column">
          <div class="img-wrapper">
            <img
              :src="product.thumbnail"
              class="product-img"
              alt="Product Image"
            />
          </div>

          <div class="card-body-custom flex-grow-1 text-center px-3 py-3">
            <h5 class="fw-bold text-dark mb-1 title-limit">
              {{ product.title }}
            </h5>
            <small class="text-muted">{{ product.category }}</small>
          </div>

          <div
            class="card-footer-custom px-3 py-3 d-flex justify-content-between align-items-center"
          >
            <div class="badge-price"><small>$</small>{{ product.price }}</div>

            <button type="button" class="btn-3d btn-3d-primary px-3 py-2">
              🛒 Add
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  setup() {
    const products = ref([]);

    const fetchProducts = async () => {
      try {
        const response = await fetch("https://dummyjson.com/products");
        const data = await response.json();
        products.value = data.products;
      } catch (error) {
        console.error("Error fetching products:", error);
      }
    };

    onMounted(fetchProducts);

    return {
      products,
    };
  },
};
</script>

<style scoped>
.text-gradient {
  background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
.title-3d {
  text-shadow: 2px 2px 4px rgba(0, 195, 255, 0.2);
  font-size: 2.5rem;
}

.card-3d {
  background: rgba(255, 255, 255, 0.65);
  backdrop-filter: blur(15px);
  -webkit-backdrop-filter: blur(15px);
  border-radius: 24px;
  border: 1px solid rgba(255, 255, 255, 0.9);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.05),
    inset 0 2px 0 rgba(255, 255, 255, 1);
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  overflow: hidden;
}

.card-3d:hover {
  transform: translateY(-10px);
  box-shadow: 0 25px 45px rgba(0, 0, 0, 0.1),
    inset 0 2px 0 rgba(255, 255, 255, 1);
  background: rgba(255, 255, 255, 0.9);
}

.img-wrapper {
  background: linear-gradient(to bottom, #fdfbfb 0%, #ebedee 100%);
  padding: 1.5rem;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 220px;
  overflow: hidden;
}

.product-img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  transition: transform 0.5s ease;
  filter: drop-shadow(0 10px 10px rgba(0, 0, 0, 0.1));
}

.card-3d:hover .product-img {
  transform: scale(1.15) rotate(3deg);
}

.title-limit {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
  min-height: 48px;
}

.card-footer-custom {
  background: transparent;
  border-top: 1px solid rgba(0, 0, 0, 0.05);
}

.badge-price {
  background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%);
  color: white;
  padding: 6px 14px;
  border-radius: 12px;
  font-weight: 700;
  font-size: 1.1rem;
  box-shadow: 0 6px 12px rgba(56, 239, 125, 0.3),
    inset 0 2px 3px rgba(255, 255, 255, 0.4);
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.15);
}
.badge-price small {
  font-size: 0.8rem;
  margin-right: 2px;
  opacity: 0.9;
}

.btn-3d {
  border: none;
  border-radius: 12px;
  font-weight: 700;
  font-size: 0.95rem;
  transition: all 0.15s ease-in-out;
  cursor: pointer;
}
.btn-3d-primary {
  background: linear-gradient(to bottom, #4facfe, #00f2fe);
  color: white;
  box-shadow: 0 4px 0 #00b4d8, 0 10px 15px rgba(0, 242, 254, 0.3);
}
.btn-3d-primary:active {
  transform: translateY(4px);
  box-shadow: 0 0px 0 #00b4d8, 0 5px 10px rgba(0, 242, 254, 0.2);
}
</style>

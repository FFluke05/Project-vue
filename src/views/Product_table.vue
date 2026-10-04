<template>
  <div class="container d-flex justify-content-center pb-5 mt-5">
    <div class="product-card-3d p-4 p-md-5 w-100">
      <h2 class="text-center fw-bold text-gradient title-3d mb-4">
        แสดงข้อมูลสินค้า
      </h2>

      <div class="text-center mb-4">
        <button
          class="btn-3d btn-3d-primary px-4 py-2"
          @click="fetchProducts"
          :disabled="isLoading"
        >
          <span :class="{ 'spin-icon': isLoading }" class="d-inline-block me-1"
            >🔄</span
          >
          {{ isLoading ? "กำลังอัปเดต..." : "อัปเดตสินค้า" }}
        </button>
      </div>

      <!-- ตารางแสดงข้อมูลแบบ Floating Rows -->
      <div class="table-responsive">
        <table class="table-glass text-center w-100 align-middle">
          <thead>
            <tr>
              <th>รหัส</th>
              <th>รูปภาพ</th>
              <th class="text-start">ชื่อสินค้า</th>
              <th>คงเหลือ</th>
              <th>ราคา</th>
            </tr>
          </thead>
          <tbody>
            <!-- v-for ใช้วนลูปข้อมูล -->
            <tr v-for="item in products" :key="item.id" class="row-3d">
              <!-- รหัสสินค้า -->
              <td class="fw-bold text-secondary-custom fs-5">
                {{ item.id }}
              </td>

              <!-- รูปสินค้า -->
              <td>
                <img
                  :src="item.thumbnail"
                  class="product-img-3d"
                  alt="Product Image"
                />
              </td>

              <!-- ชื่อสินค้า -->
              <td class="text-start fw-bold text-dark fs-6">
                {{ item.title }}
              </td>

              <!-- จำนวนคงเหลือ -->
              <td>
                <div class="badge-3d badge-stock">
                  {{ item.stock }} <small>ชิ้น</small>
                </div>
              </td>

              <!-- ราคาขาย -->
              <td>
                <div class="badge-3d badge-price">
                  <small>$</small>{{ item.price }}
                </div>
              </td>
            </tr>

            <tr v-if="products.length === 0 && !isLoading">
              <td colspan="5" class="text-muted py-5 fs-5">
                ไม่พบข้อมูลสินค้า
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  setup() {

    const products = ref([]);
    const isLoading = ref(false);

    const fetchProducts = async () => {
      isLoading.value = true;
      try {
        const response = await fetch("https://dummyjson.com/products");
        const data = await response.json();
        products.value = data.products;
      } catch (error) {
        console.error("Error fetching products:", error);
      } finally {

        setTimeout(() => {
          isLoading.value = false;
        }, 500);
      }
    };

    onMounted(fetchProducts);

    return {
      products,
      isLoading, 
      fetchProducts,
    };
  },
};
</script>

<style scoped>
/* --- Glassmorphism Card --- */
.product-card-3d {
  background: rgba(255, 255, 255, 0.7);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-radius: 24px;
  border: 1px solid rgba(255, 255, 255, 0.9);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.08),
    inset 0 2px 0 rgba(255, 255, 255, 1);
  max-width: 1000px;
}

/* --- หัวข้อ (Text 3D) --- */
.text-gradient {
  background: linear-gradient(135deg, #a18cd1 0%, #fbc2eb 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.title-3d {
  text-shadow: 2px 2px 4px rgba(161, 140, 209, 0.3);
  font-size: 2.5rem;
}

.text-secondary-custom {
  color: #5a6a80;
}

/* --- ปุ่ม 3 มิติ --- */
.btn-3d {
  border: none;
  border-radius: 12px;
  font-weight: 600;
  font-size: 1.1rem;
  transition: all 0.15s ease-in-out;
}

.btn-3d-primary {
  background: linear-gradient(to bottom, #4facfe, #00f2fe);
  color: white;
  box-shadow: 0 6px 0 #00b4d8, 0 15px 20px rgba(0, 242, 254, 0.3);
}

.btn-3d-primary:active:not(:disabled) {
  transform: translateY(6px);
  box-shadow: 0 0px 0 #00b4d8, 0 5px 10px rgba(0, 242, 254, 0.2);
}

.btn-3d-primary:disabled {
  opacity: 0.8;
  cursor: not-allowed;
}

/* ไอคอนหมุนตอนโหลด */
.spin-icon {
  animation: spin 1s linear infinite;
}

@keyframes spin {
  100% {
    transform: rotate(360deg);
  }
}

/* --- ตารางแบบ 3 มิติ (Floating Rows) --- */
.table-glass {
  border-collapse: separate;
  border-spacing: 0 12px;
}

.table-glass th {
  border: none;
  color: #8c98a4;
  font-weight: 600;
  padding: 10px 15px;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.row-3d {
  background: rgba(255, 255, 255, 0.8);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.04), inset 0 1px 0 white;
  transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275),
    box-shadow 0.3s ease;
}

.row-3d td {
  border: none;
  padding: 15px;
}

.row-3d td:first-child {
  border-radius: 16px 0 0 16px;
}

.row-3d td:last-child {
  border-radius: 0 16px 16px 0;
}

.row-3d:hover {
  transform: translateY(-4px) scale(1.01);
  box-shadow: 0 15px 25px rgba(0, 0, 0, 0.1), inset 0 1px 0 white;
  background: rgba(255, 255, 255, 1);
}

/* --- รูปภาพ 3 มิติ --- */
.product-img-3d {
  width: 80px;
  height: 80px;
  object-fit: cover;
  border-radius: 12px;
  background-color: #f8f9fa;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1),
    inset 0 2px 4px rgba(255, 255, 255, 1);
  padding: 5px;
  transition: transform 0.3s ease;
}

.row-3d:hover .product-img-3d {
  transform: scale(1.1) rotate(2deg);
}

/* --- ป้ายข้อมูล 3 มิติ --- */
.badge-3d {
  display: inline-block;
  padding: 6px 16px;
  border-radius: 12px;
  font-weight: 700;
  font-size: 1rem;
  letter-spacing: 0.5px;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.1),
    inset 0 2px 3px rgba(255, 255, 255, 0.4);
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.15);
  color: white;
}

.badge-3d small {
  font-size: 0.8rem;
  opacity: 0.9;
}

/* สีป้ายสต็อก (ส้ม/เหลือง) */
.badge-stock {
  background: linear-gradient(135deg, #f6d365 0%, #fda085 100%);
}

/* สีป้ายราคา (เขียว) */
.badge-price {
  background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%);
}
</style>

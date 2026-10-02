<template>
    <div class="container d-flex justify-content-center pb-5 mt-5">

        <!-- การ์ดกระจก -->
        <div class="gold-card-3d p-4 p-md-5 w-100">

            <h2 class="text-center fw-bold text-gradient title-3d mb-4">💰 ราคาทองวันนี้</h2>

            <!-- ปุ่มกดเพื่อดึงข้อมูล -->
            <div class="text-center mb-4">
                <button class="btn-3d btn-3d-primary px-4 py-2" @click="fetchGold" :disabled="isLoading">
                    <span :class="{ 'spin-icon': isLoading }" class="d-inline-block me-1">🔄</span>
                    {{ isLoading ? 'กำลังอัปเดต...' : 'อัปเดตราคา' }}
                </button>
            </div>

            <!-- ตารางแสดงข้อมูลแบบ Floating Rows -->
            <div class="table-responsive">
                <table class="table-glass text-center w-100">
                    <thead>
                        <tr>
                            <th>ประเภททอง</th>
                            <th>ราคารับซื้อ</th>
                            <th>ราคาขายออก</th>
                        </tr>
                    </thead>
                    <tbody>
                        <!-- v-for ใช้วนลูปข้อมูลใน golds -->
                        <tr v-for="item in golds" :key="item.name" class="row-3d">
                            <td class="fw-bold text-secondary-custom fs-5">{{ item.name }}</td>

                            <!-- ราคาซื้อ -->
                            <td>
                                <div class="price-badge price-buy">
                                    {{ formatNumber(item.buy) }} <small>บาท</small>
                                </div>
                            </td>

                            <!-- ราคาขาย -->
                            <td>
                                <div class="price-badge price-sell">
                                    {{ formatNumber(item.sell) }} <small>บาท</small>
                                </div>
                            </td>
                        </tr>

                        <!-- แสดงสถานะกำลังโหลดถ้าข้อมูลยังไม่มี -->
                        <tr v-if="golds.length === 0 && !isLoading">
                            <td colspan="3" class="text-muted py-4">ไม่พบข้อมูลราคาทอง</td>
                        </tr>
                    </tbody>
                </table>
            </div>

        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const golds = ref([])
const isLoading = ref(false) // เพิ่มตัวแปรสำหรับสถานะโหลดข้อมูล

const fetchGold = async () => {
    isLoading.value = true
    try {
        const res = await fetch('https://api.chnwt.dev/thai-gold-api/latest')
        const data = await res.json()
        const price = data.response.price

        golds.value = [
            {
                name: "ทองรูปพรรณ",
                buy: parseFloat(price.gold.buy.replace(/,/g, "")),
                sell: parseFloat(price.gold.sell.replace(/,/g, ""))
            },
            {
                name: "ทองคำแท่ง",
                buy: parseFloat(price.gold_bar.buy.replace(/,/g, "")),
                sell: parseFloat(price.gold_bar.sell.replace(/,/g, ""))
            }
        ]
    } catch (error) {
        console.error("โหลดข้อมูลผิดพลาด:", error)
    } finally {
        setTimeout(() => { isLoading.value = false }, 500)
    }
}

const formatNumber = (num) => {
    return num.toLocaleString()
}

onMounted(fetchGold)
</script>

<style scoped>
/* --- Glassmorphism Card --- */
.gold-card-3d {
    background: rgba(255, 255, 255, 0.7);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border-radius: 24px;
    border: 1px solid rgba(255, 255, 255, 0.9);
    box-shadow:
        0 20px 40px rgba(0, 0, 0, 0.08),
        inset 0 2px 0 rgba(255, 255, 255, 1);
    max-width: 800px;
}

/* --- หัวข้อ (Text 3D) --- */
.text-gradient {
    background: linear-gradient(135deg, #f6d365 0%, #fda085 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
}

.title-3d {
    text-shadow: 2px 2px 4px rgba(253, 160, 133, 0.3);
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
    /* เว้นระยะห่างระหว่างแถว */
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
    transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275), box-shadow 0.3s ease;
}

.row-3d td {
    border: none;
    padding: 20px 15px;
    vertical-align: middle;
}

/* ทำขอบมนให้ช่องซ้ายสุดและขวาสุดของตาราง */
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

/* --- ป้ายราคา 3 มิติ (Price Badges) --- */
.price-badge {
    display: inline-block;
    padding: 8px 20px;
    border-radius: 12px;
    font-weight: 700;
    font-size: 1.2rem;
    letter-spacing: 0.5px;
    box-shadow:
        0 8px 15px rgba(0, 0, 0, 0.1),
        inset 0 2px 3px rgba(255, 255, 255, 0.4);
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.15);
}

.price-badge small {
    font-size: 0.85rem;
    opacity: 0.9;
}

.price-buy {
    background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%);
    color: white;
}

.price-sell {
    background: linear-gradient(135deg, #ff416c 0%, #ff4b2b 100%);
    color: white;
}
</style>
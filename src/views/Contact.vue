<template>
  <div class="container d-flex justify-content-center pb-5 mt-5">

    <!-- การ์ดกระจก 3 มิติ -->
    <div class="auth-card-3d p-5 text-center">

      <!-- ไอคอนสถานะแบบ 3 มิติ ลอยตัว -->
      <div class="icon-3d mb-4" :class="{ 'icon-unlocked': isLoggedIn, 'icon-locked': !isLoggedIn }">
        {{ isLoggedIn ? '🔓' : '🔒' }}
      </div>

      <!-- แสดงข้อความไล่สีแบบ 3 มิติ -->
      <h1 class="display-5 fw-bold text-gradient mb-4 title-3d">
        {{ isLoggedIn ? 'ยินดีต้อนรับ!' : 'กรุณาเข้าสู่ระบบ' }}
      </h1>

      <!-- ปุ่ม 3 มิติ ใช้ :class เพื่อเปลี่ยนสีตามสถานะ -->
      <button @click="toggleLogin"
        :class="['btn-3d', 'btn-lg', 'px-5', isLoggedIn ? 'btn-3d-danger' : 'btn-3d-primary']">
        {{ isLoggedIn ? 'ออกจากระบบ' : 'เข้าสู่ระบบ' }}
      </button>

    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isLoggedIn: false, // ตัวแปรสำหรับเก็บสถานะการเข้าสู่ระบบ
    };
  },
  methods: {
    toggleLogin() {
      this.isLoggedIn = !this.isLoggedIn; // สลับค่าสถานะ
    },
  },
};
</script>

<style scoped>
.auth-card-3d {
  background: rgba(255, 255, 255, 0.7);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-radius: 30px;
  border: 1px solid rgba(255, 255, 255, 0.9);
  box-shadow:
    0 20px 40px rgba(0, 0, 0, 0.1),
    inset 0 2px 0 rgba(255, 255, 255, 1);
  max-width: 500px;
  width: 100%;
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  transform-style: preserve-3d;
}

.auth-card-3d:hover {
  transform: translateY(-5px);
  box-shadow: 0 30px 50px rgba(0, 0, 0, 0.15);
}

.icon-3d {
  font-size: 4rem;
  display: inline-block;
  transition: transform 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  filter: drop-shadow(0 10px 10px rgba(0, 0, 0, 0.2));
}

.icon-locked {
  transform: scale(1);
}

.icon-unlocked {
  transform: scale(1.1) rotate(10deg);
}

.text-gradient {
  background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.title-3d {
  text-shadow:
    2px 2px 0px rgba(0, 195, 255, 0.2),
    4px 4px 10px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.btn-3d {
  border: none;
  border-radius: 16px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  transition: all 0.15s ease-in-out;
  cursor: pointer;
  outline: none;
}

.btn-3d-primary {
  background: linear-gradient(to bottom, #4facfe, #00f2fe);
  color: white;
  box-shadow:
    0 8px 0 #00b4d8,
    0 15px 20px rgba(0, 242, 254, 0.4);
}

.btn-3d-primary:active {
  transform: translateY(8px);
  box-shadow: 0 0px 0 #00b4d8, 0 5px 10px rgba(0, 242, 254, 0.3);
}

.btn-3d-danger {
  background: linear-gradient(to bottom, #ff416c, #ff4b2b);
  color: white;
  box-shadow:
    0 8px 0 #c22944,
    0 15px 20px rgba(255, 65, 108, 0.4);
}

.btn-3d-danger:active {
  transform: translateY(8px);
  box-shadow: 0 0px 0 #c22944, 0 5px 10px rgba(255, 65, 108, 0.3);
}
</style>

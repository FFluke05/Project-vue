<template>
  <div class="container d-flex justify-content-center pb-5 mt-5">

    <!-- การ์ด 3 มิติ -->
    <div class="grade-card-3d p-4 p-md-5 text-center">
      <h2 class="fw-bold text-gradient title-3d mb-4">ระบบตัดเกรด</h2>

      <!-- Input สำหรับรับคะแนนแบบ 3 มิติ -->
      <div class="mb-4">
        <input type="number" class="form-control form-control-lg input-3d text-center" v-model="score"
          placeholder="กรอกคะแนน (0-100)" @keyup.enter="calculateGrade" />
      </div>

      <!-- ปุ่มคำนวณเกรด 3 มิติ -->
      <button class="btn-3d btn-3d-primary btn-lg px-5 w-100 mb-4" @click="calculateGrade">
        คำนวณเกรด
      </button>

      <!-- พื้นที่แสดงผลลัพธ์ -->
      <div class="result-area" style="min-height: 140px;">
        <!-- แสดงผลลัพธ์เกรด พร้อมอนิเมชันเด้ง -->
        <div v-if="grade !== ''" class="result-3d animate-pop">
          <span class="text-secondary-custom fw-medium">เกรดของคุณคือ</span>
          <div class="grade-badge-3d mt-2 mx-auto" :class="'grade-' + grade">
            {{ grade }}
          </div>
        </div>

        <!-- แสดงข้อความแจ้งเตือนเมื่อมีข้อผิดพลาด พร้อมอนิเมชันสั่น -->
        <div v-if="errorMessage" class="error-3d animate-shake mt-3 p-3">
          ⚠️️ {{ errorMessage }}
        </div>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      score: '',      // เก็บค่าคะแนนจากผู้ใช้
      grade: '',      // เก็บผลลัพธ์เกรดที่คำนวณได้
      errorMessage: '' // ข้อความแจ้งเตือนเมื่อเกิดข้อผิดพลาด
    }
  },
  methods: {
    calculateGrade() {
      // ตรวจสอบว่าผู้ใช้กรอกคะแนนหรือไม่
      if (this.score === '') {
        this.errorMessage = 'กรุณากรอกคะแนนก่อนคำนวณ';
        this.grade = '';
        return;
      }

      // แปลง score เป็นตัวเลข
      const score = Number(this.score);

      // ตรวจสอบว่าคะแนนเกิน 100 หรือน้อยกว่า 0 หรือไม่
      if (score > 100 || score < 0) {
        this.errorMessage = 'กรุณากรอกคะแนนให้ถูกต้อง (0-100)';
        this.grade = '';
        return;
      }

      // รีเซ็ตข้อความแจ้งเตือน
      this.errorMessage = '';

      // ตรวจสอบคะแนนและกำหนดเกรด
      if (score >= 80) {
        this.grade = 'A';
      } else if (score >= 70) {
        this.grade = 'B';
      } else if (score >= 60) {
        this.grade = 'C';
      } else if (score >= 50) {
        this.grade = 'D';
      } else {
        this.grade = 'F';
      }
    }
  }
}
</script>

<style scoped>

.grade-card-3d {
  background: rgba(255, 255, 255, 0.75);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-radius: 24px;
  border: 1px solid rgba(255, 255, 255, 0.9);
  box-shadow:
    0 20px 40px rgba(0, 0, 0, 0.08),
    inset 0 2px 0 rgba(255, 255, 255, 1);
  max-width: 450px;
  width: 100%;
}

.text-gradient {
  background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.title-3d {
  text-shadow: 2px 2px 4px rgba(0, 195, 255, 0.2);
}

.text-secondary-custom {
  color: #5a6a80;
}

.input-3d {
  background-color: #f8f9fa;
  border: none !important;
  border-radius: 16px !important;
  box-shadow:
    inset 0 4px 8px rgba(0, 0, 0, 0.08),
    inset 0 1px 3px rgba(0, 0, 0, 0.1),
    0 1px 0 rgba(255, 255, 255, 1) !important;
  transition: all 0.3s ease;
  font-size: 1.25rem;
  font-weight: 600;
  color: #333;
}

.input-3d:focus {
  background-color: #ffffff;
  box-shadow:
    inset 0 2px 4px rgba(0, 195, 255, 0.1),
    0 0 0 4px rgba(79, 172, 254, 0.25) !important;
  outline: none;
}

.input-3d::-webkit-outer-spin-button,
.input-3d::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

.btn-3d {
  border: none;
  border-radius: 16px;
  font-weight: 700;
  font-size: 1.1rem;
  transition: all 0.15s ease-in-out;
  cursor: pointer;
}

.btn-3d-primary {
  background: linear-gradient(to bottom, #4facfe, #00f2fe);
  color: white;
  box-shadow: 0 8px 0 #00b4d8, 0 15px 20px rgba(0, 242, 254, 0.4);
}

.btn-3d-primary:active {
  transform: translateY(8px);
  box-shadow: 0 0px 0 #00b4d8, 0 5px 10px rgba(0, 242, 254, 0.3);
}

.grade-badge-3d {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 90px;
  height: 90px;
  font-size: 3.5rem;
  font-weight: 800;
  color: white;
  border-radius: 24px;
  background: linear-gradient(135deg, #00c6ff 0%, #0072ff 100%);
  box-shadow:
    0 15px 25px rgba(0, 114, 255, 0.4),
    inset 0 4px 5px rgba(255, 255, 255, 0.5),
    inset 0 -4px 5px rgba(0, 0, 0, 0.1);
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
}

.grade-A {
  background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%);
  box-shadow: 0 15px 25px rgba(56, 239, 125, 0.4), inset 0 4px 5px rgba(255, 255, 255, 0.5);
}

.grade-B {
  background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
  box-shadow: 0 15px 25px rgba(0, 242, 254, 0.4), inset 0 4px 5px rgba(255, 255, 255, 0.5);
}

.grade-C {
  background: linear-gradient(135deg, #b224ef 0%, #7579ff 100%);
  box-shadow: 0 15px 25px rgba(117, 121, 255, 0.4), inset 0 4px 5px rgba(255, 255, 255, 0.5);
}

.grade-D {
  background: linear-gradient(135deg, #f6d365 0%, #fda085 100%);
  box-shadow: 0 15px 25px rgba(253, 160, 133, 0.4), inset 0 4px 5px rgba(255, 255, 255, 0.5);
}

.grade-F {
  background: linear-gradient(135deg, #ff416c 0%, #ff4b2b 100%);
  box-shadow: 0 15px 25px rgba(255, 65, 108, 0.4), inset 0 4px 5px rgba(255, 255, 255, 0.5);
}

.error-3d {
  background: #fff3f3;
  color: #dc3545;
  font-weight: 600;
  border-radius: 12px;
  box-shadow: 0 5px 15px rgba(220, 53, 69, 0.15), inset 0 0 0 1px rgba(220, 53, 69, 0.2);
}

.animate-pop {
  animation: popIn 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55) forwards;
}

@keyframes popIn {
  0% {
    opacity: 0;
    transform: scale(0.5) translateY(20px);
  }

  100% {
    opacity: 1;
    transform: scale(1) translateY(0);
  }
}

.animate-shake {
  animation: shake 0.4s ease-in-out;
}

@keyframes shake {

  0%,
  100% {
    transform: translateX(0);
  }

  25% {
    transform: translateX(-8px);
  }

  50% {
    transform: translateX(8px);
  }

  75% {
    transform: translateX(-4px);
  }
}
</style>
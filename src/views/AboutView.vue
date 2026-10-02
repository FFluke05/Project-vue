<template>
  <div class="container my-5 d-flex justify-content-center">
    <div class="profile-card-3d p-5 text-center">
      <h1 class="display-4 fw-bold text-gradient name-3d mb-3">Patipan Phodee</h1>
      <h3 class="subtitle-3d d-inline-block px-4 py-2 mt-2">ทดสอบ</h3>
    </div>
  </div>
</template>

<style scoped>

.profile-card-3d {
  background: rgba(255, 255, 255, 0.65);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-radius: 30px;
  border: 1px solid rgba(255, 255, 255, 0.9);
  box-shadow:
    0 25px 50px rgba(0, 0, 0, 0.08),
    inset 0 2px 0 rgba(255, 255, 255, 1),
    inset 0 -2px 5px rgba(0, 0, 0, 0.05);
  transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275), box-shadow 0.4s ease;
  transform-style: preserve-3d;
  max-width: 600px;
  width: 100%;
  animation: float-profile 5s ease-in-out infinite;
}

.profile-card-3d:hover {
  transform: translateY(-10px) rotateX(5deg) rotateY(-5deg);
  box-shadow:
    15px 25px 40px rgba(0, 0, 0, 0.12),
    -5px -5px 15px rgba(255, 255, 255, 0.8);
}

@keyframes float-profile {
  0% {
    transform: translateY(0px);
  }

  50% {
    transform: translateY(-12px);
  }

  100% {
    transform: translateY(0px);
  }
}

.text-gradient {
  background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.name-3d {
  position: relative;
  text-shadow:
    2px 2px 0px rgba(0, 195, 255, 0.2),
    4px 4px 8px rgba(0, 0, 0, 0.15);
  transition: transform 0.3s ease;
}


.subtitle-3d {
  background: #f0f2f5;
  color: #5a6a80;
  border-radius: 50px;
  font-weight: 600;
  letter-spacing: 1.5px;
  box-shadow:
    6px 6px 12px rgba(0, 0, 0, 0.08),
    -6px -6px 12px rgba(255, 255, 255, 1),
    inset 0 1px 1px rgba(255, 255, 255, 0.5);
  transition: all 0.3s ease;
  cursor: default;
}

.subtitle-3d:hover {
  color: #00f2fe;
  transform: scale(1.05);
  box-shadow:
    8px 8px 15px rgba(0, 0, 0, 0.1),
    -8px -8px 15px rgba(255, 255, 255, 1);
}
</style>

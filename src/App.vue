<template>
  <div class="navbar-wrapper">
    <nav class="navbar navbar-expand-lg navbar-glass">
      <div class="container">
        <a class="navbar-brand fw-bold text-gradient brand-3d" href="#">Navbar</a>

        <button class="navbar-toggler toggler-3d" type="button" data-bs-toggle="collapse"
          data-bs-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false"
          aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarNavDropdown">
          <ul class="navbar-nav ms-auto gap-2">
            <li class="nav-item">
              <a class="nav-link nav-link-3d active" aria-current="page" href="/">Home</a>
            </li>
            <li class="nav-item">
              <a class="nav-link nav-link-3d" href="/about">About</a>
            </li>
            <li class="nav-item">
              <a class="nav-link nav-link-3d" href="/contact">Contact</a>
            </li>
            <li class="nav-item dropdown">
              <a class="nav-link nav-link-3d dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown"
                aria-expanded="false">
                Dropdown link
              </a>
              <ul class="dropdown-menu dropdown-3d">
                <li><a class="dropdown-item item-3d" href="#">Action</a></li>
                <li><a class="dropdown-item item-3d" href="#">Another action</a></li>
                <li>
                  <hr class="dropdown-divider hr-3d">
                </li>
                <li><a class="dropdown-item item-3d" href="#">Something else here</a></li>
              </ul>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </div>

  <!-- หน้าแสดงเพจที่เลือก เมนู -->
  <router-view />
</template>

<style scoped>
.navbar-wrapper {
  padding: 1rem 1rem 0;
  position: sticky;
  top: 0;
  z-index: 1000;
}

.navbar-glass {
  background: rgba(255, 255, 255, 0.65);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid rgba(255, 255, 255, 0.8);
  border-radius: 20px;
  box-shadow:
    0 15px 35px rgba(0, 0, 0, 0.05),
    inset 0 1px 0 rgba(255, 255, 255, 1);
  transition: all 0.3s ease;
}

.text-gradient {
  background: linear-gradient(45deg, #4facfe 0%, #00f2fe 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.brand-3d {
  font-size: 1.5rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.brand-3d:hover {
  transform: scale(1.05) translateY(-2px);
}

.nav-link-3d {
  font-weight: 600;
  color: #5a6a80 !important;
  border-radius: 12px;
  padding: 0.5rem 1rem !important;
  transition: all 0.3s ease;
  position: relative;
}

.nav-link-3d:hover {
  color: #00f2fe !important;
  background: rgba(255, 255, 255, 0.8);
  box-shadow:
    0 5px 10px rgba(0, 0, 0, 0.05),
    inset 0 1px 0 rgba(255, 255, 255, 1);
  transform: translateY(-2px);
}

.nav-link-3d.active {
  color: white !important;
  background: linear-gradient(to bottom, #4facfe, #00f2fe);
  box-shadow:
    0 4px 0 #00b4d8,
    0 10px 15px rgba(0, 242, 254, 0.3);
}

.nav-link-3d.active:active {
  transform: translateY(4px);
  box-shadow: 0 0px 0 #00b4d8, 0 5px 10px rgba(0, 242, 254, 0.3);
}

.toggler-3d {
  border: none;
  background: rgba(255, 255, 255, 0.7);
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05), inset 0 1px 0 white;
  padding: 0.5rem;
}

.dropdown-3d {
  border: none;
  background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(10px);
  border-radius: 16px;
  padding: 0.5rem;
  margin-top: 10px;
  box-shadow:
    0 20px 40px rgba(0, 0, 0, 0.1),
    inset 0 1px 0 rgba(255, 255, 255, 1),
    0 0 0 1px rgba(255, 255, 255, 0.5);
  animation: dropdownFade 0.3s ease;
}

@keyframes dropdownFade {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.item-3d {
  border-radius: 8px;
  transition: all 0.2s ease;
  color: #5a6a80;
  font-weight: 500;
  margin-bottom: 2px;
}

.item-3d:hover {
  background: #f8f9fa;
  color: #00f2fe;
  transform: translateX(5px);
  box-shadow: -3px 3px 10px rgba(0, 0, 0, 0.05);
}

.hr-3d {
  margin: 0.5rem 0;
  border-color: rgba(0, 0, 0, 0.05);
}

.main-content {
  padding-top: 2rem;
}
</style>
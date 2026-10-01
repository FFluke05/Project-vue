<template>
  <div class="super-container">
    <div class="container pb-5">

      <div class="px-4 py-5 my-5 text-center hero-section">
        <img class="d-block mx-auto mb-4 floating-element" src="../assets/image/ima1.svg" alt="Hero Icon" width="80"
          height="80">
        <h1 class="display-5 fw-bold text-gradient">Centered hero</h1>
        <div class="col-lg-6 mx-auto">
          <p class="lead mb-4 text-secondary-custom">
            Quickly design and customize responsive mobile-first sites with Bootstrap, the world’s most
            popular front-end open source toolkit, featuring Sass variables and mixins.
          </p>
          <div class="d-grid gap-3 d-sm-flex justify-content-sm-center mt-5">
            <button type="button" class="btn-3d btn-3d-primary btn-lg px-5">Primary action</button>
            <button type="button" class="btn-3d btn-3d-secondary btn-lg px-5">Secondary</button>
          </div>
        </div>
      </div>

      <div class="container col-xl-10 col-xxl-8 px-4 py-5 mt-5">
        <div class="row align-items-center g-lg-5 py-5">

          <div class="col-lg-7 text-center text-lg-start pe-lg-5">
            <h1 class="display-4 fw-bold lh-1 mb-4 text-gradient">Vertically centered hero sign-up form</h1>
            <p class="fs-4 text-secondary-custom">
              Below is an example form built entirely with Bootstrap’s form controls. Each
              required form group has a validation state that can be triggered.
            </p>
          </div>

          <div class="col-md-10 mx-auto col-lg-5">
            <form class="p-4 p-md-5 bg-white card-3d">
              <div class="form-floating mb-4">
                <input type="email" class="form-control input-3d" id="floatingInput" placeholder="name@example.com">
                <label for="floatingInput">Email address</label>
              </div>
              <div class="form-floating mb-4">
                <input type="password" class="form-control input-3d" id="floatingPassword" placeholder="Password">
                <label for="floatingPassword">Password</label>
              </div>
              <div class="checkbox mb-4 custom-checkbox">
                <label>
                  <input type="checkbox" value="remember-me" class="checkbox-3d"> Remember me
                </label>
              </div>
              <button class="w-100 btn-3d btn-3d-primary btn-lg" type="submit">Sign up</button>
              <hr class="my-4 hr-3d">
              <small class="text-muted fw-medium">By clicking Sign up, you agree to the terms of use.</small>
            </form>
          </div>

        </div>
      </div>

    </div>
  </div>
</template>

<style scoped>

.super-container {
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
  min-height: 100vh;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  overflow-x: hidden;
}

.text-gradient {
  background: linear-gradient(45deg, #4facfe 0%, #00f2fe 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
}

.text-secondary-custom {
  color: #5a6a80;
  text-shadow: 1px 1px 2px rgba(255, 255, 255, 0.8);
}

.floating-element {
  animation: float 4s ease-in-out infinite;
  filter: drop-shadow(0 15px 15px rgba(0, 150, 255, 0.3));
}

@keyframes float {
  0% {
    transform: translateY(0px);
  }

  50% {
    transform: translateY(-15px);
  }

  100% {
    transform: translateY(0px);
  }
}

.btn-3d {
  position: relative;
  border: none;
  border-radius: 12px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1px;
  transition: all 0.1s ease-in-out;
  cursor: pointer;
  outline: none;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.btn-3d-primary {
  background: linear-gradient(to bottom, #4facfe, #00f2fe);
  color: white;
  box-shadow: 0 6px 0 #00b4d8, 0 15px 20px rgba(0, 242, 254, 0.4);
}

.btn-3d-primary:active {
  transform: translateY(6px);
  box-shadow: 0 0px 0 #00b4d8, 0 5px 10px rgba(0, 242, 254, 0.3);
}

.btn-3d-secondary {
  background: linear-gradient(to bottom, #ffffff, #f1f3f5);
  color: #495057;
  box-shadow: 0 6px 0 #ced4da, 0 15px 20px rgba(0, 0, 0, 0.1);
}

.btn-3d-secondary:active {
  transform: translateY(6px);
  box-shadow: 0 0px 0 #ced4da, 0 5px 10px rgba(0, 0, 0, 0.1);
}

.card-3d {
  border-radius: 24px !important;
  border: 1px solid rgba(255, 255, 255, 0.8);
  box-shadow:
    0 20px 40px rgba(0, 0, 0, 0.08),
    0 1px 3px rgba(0, 0, 0, 0.05),
    inset 0 0 0 1px rgba(255, 255, 255, 0.5);
  backdrop-filter: blur(10px);
  transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275), box-shadow 0.4s ease;
  transform-style: preserve-3d;
  perspective: 1000px;
}

.card-3d:hover {
  transform: translateY(-10px) rotateX(2deg) rotateY(-2deg);
  box-shadow:
    20px 30px 50px rgba(0, 0, 0, 0.12),
    0 5px 15px rgba(0, 0, 0, 0.08);
}

.input-3d {
  background-color: #f8f9fa;
  border: none !important;
  border-radius: 12px !important;
  box-shadow: inset 0 4px 6px rgba(0, 0, 0, 0.06),
    inset 0 1px 3px rgba(0, 0, 0, 0.08),
    0 1px 0 rgba(255, 255, 255, 1) !important;
  transition: all 0.3s ease;
}

.input-3d:focus {
  background-color: #ffffff;
  box-shadow: inset 0 2px 4px rgba(0, 195, 255, 0.1),
    0 0 0 4px rgba(79, 172, 254, 0.25) !important;
}

.checkbox-3d {
  width: 18px;
  height: 18px;
  accent-color: #00f2fe;
  cursor: pointer;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.hr-3d {
  border: 0;
  height: 2px;
  background: linear-gradient(to right, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.1), rgba(0, 0, 0, 0));
}
</style>

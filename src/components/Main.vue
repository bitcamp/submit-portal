<script setup></script>

<template>
  <div class="dinos-wrapper">
    <img
      src="../assets/img/images/bitcamp-dinos.svg"
      width="300"
      alt="Bitcamp"
    />
  </div>

  <div class="d-flex justify-content-center align-items-center vh-100">
    <b-card class="main-card text-center">
      <b-button class="submit-btn" variant="primary">Submit</b-button>
    </b-card>
  </div>
</template>

<style scoped>
.dinos-wrapper {
  position: absolute;
  top: 3rem;
  left: 50%;
  transform: translateX(-50%);
}

@property --angle {
  syntax: "<angle>";
  initial-value: 0deg;
  inherits: false;
}

.main-card {
  display: inline-block !important;
  background-color: var(--color-midnight) !important;
  border: none !important;
  border-radius: 1rem !important;
  padding: 0 !important;
  overflow: visible !important;
}

.submit-btn {
  position: relative;
  padding: 2rem 8rem !important;
  font-size: 2.5rem !important;
  font-weight: 700 !important;
  font-family: var(--font-aleo), serif;
  letter-spacing: 0.05em;
  border: none !important;
  border-radius: 1rem !important;
  background: linear-gradient(
    135deg,
    var(--color-bitcamp),
    var(--color-flame)
  ) !important;
  color: var(--color-shell) !important;
  cursor: pointer;
  transition:
    transform 0.15s ease,
    box-shadow 0.15s ease;
}

.submit-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 16px black !important;
}

.submit-btn:active {
  transform: translateY(2px) scale(0.97);
  box-shadow: none !important;
}

.submit-btn::after,
.submit-btn::before {
  content: "";
  position: absolute;
  inset: -0.25rem;
  background-image: conic-gradient(from var(--angle), transparent 50%, #f9ad4b);
  z-index: -1;
  border-radius: 1rem;
  animation: 3s spin linear infinite;
}

.submit-btn::before {
  filter: blur(0.4rem);
  opacity: 0.5;
}

@keyframes spin {
  from {
    --angle: 0deg;
  }
  to {
    --angle: 360deg;
  }
}
</style>

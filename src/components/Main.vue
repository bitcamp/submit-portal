<script setup>
import { ref } from "vue";
import { BButton, BCard, BModal } from "bootstrap-vue-next";

const showModal = ref(false);
const step = ref(1);
const devpostClicked = ref(false);
const submitting = ref(false);

const form = ref({
  teamName: "",
  submissionUrl: "",
  teamEmail: "",
  companyChallenges: [],
  trackChallenges: [],
  mlhChallenges: [],
});

const companyChallengeOptions = [
  "Capital One",
  "Bloomberg",
  "Booz Allen Hamilton",
];

const trackChallengeOptions = [
  "Health & Wellness",
  "Education",
  "Sustainability",
  "Social Good",
];

const mlhChallengeOptions = [
  "Best Use of AI",
  "Best DEI Hack",
  "Best Use of Google Cloud",
];

function openModal() {
  showModal.value = true;
  step.value = 1;
  devpostClicked.value = false;
  submitting.value = false;
}

function cancelModal() {
  showModal.value = false;
}

function goToDevpost() {
  devpostClicked.value = true;
  window.open(
    "https://bitcamp2025.devpost.com/?ref_feature=challenge&ref_medium=discover",
    "_blank",
  );
}

function nextStep() {
  step.value = 2;
}

function prevStep() {
  step.value = 1;
}

function handleSubmit() {
  submitting.value = true;
  console.log("Submitted:", form.value);
  setTimeout(() => {
    showModal.value = false;
    submitting.value = false;
  }, 1000);
}
</script>

<template>
  <div class="dinos-wrapper">
    <img
      src="../assets/img/images/logotype-mono.png"
      width="300"
      alt="Bitcamp"
    />
  </div>

  <div class="d-flex justify-content-center align-items-center vh-100">
    <b-card class="main-card text-center">
      <b-button class="submit-btn" variant="primary" @click="openModal"
        >Submit</b-button
      >
    </b-card>
  </div>

  <b-modal
    v-model="showModal"
    centered
    no-footer
    no-header
    size="lg"
    modal-class="submit-modal"
    body-class="modal-body-custom"
    :no-close-on-backdrop="submitting"
    :no-close-on-esc="submitting"
  >
    <div class="modal-inner">
      <div class="warning-banner">
        Both steps must be completed to be considered for judging. If either
        step is incomplete, your project will not be judged.
      </div>
      <!-- Step 1 -->
      <div v-if="step === 1" class="step-content">
        <div class="step-header">
          <span class="step-badge">Step 1 of 2</span>
          <h3 class="step-title">Submit to Devpost</h3>
          <p class="step-subtitle">
            First, submit your project on Devpost before continuing.
          </p>
        </div>

        <div class="devpost-area">
          <b-button class="devpost-btn" @click="goToDevpost">
            Go to Devpost
          </b-button>
          <span v-if="devpostClicked" class="devpost-check">Done</span>
        </div>

        <div class="btn-row">
          <button
            type="button"
            class="btn-secondary-custom"
            @click="cancelModal"
          >
            Cancel
          </button>
          <b-button
            class="btn-primary-custom"
            :disabled="!devpostClicked"
            @click="nextStep"
          >
            Next
          </b-button>
        </div>
      </div>

      <!-- Step 2 -->
      <div v-else class="step-content">
        <div class="step-header">
          <span class="step-badge">Step 2 of 2</span>
          <h3 class="step-title">Project Details</h3>
        </div>

        <form @submit.prevent="handleSubmit" class="form-area">
          <fieldset :disabled="submitting">
            <div class="form-row">
              <div class="form-col">
                <label class="form-label-custom">Team Name</label>
                <input
                  v-model="form.teamName"
                  type="text"
                  placeholder="Team name"
                  class="form-input-custom"
                  required
                />
              </div>
              <div class="form-col">
                <label class="form-label-custom">Team Email</label>
                <input
                  v-model="form.teamEmail"
                  type="email"
                  placeholder="team@example.com"
                  class="form-input-custom"
                  required
                />
              </div>
            </div>

            <div class="form-group-custom">
              <label class="form-label-custom">Submission URL</label>
              <input
                v-model="form.submissionUrl"
                type="url"
                placeholder="https://devpost.com/software/..."
                class="form-input-custom"
                required
              />
            </div>

            <div class="challenges-grid">
              <div class="challenge-col">
                <label class="form-label-custom">Company Challenges</label>
                <div class="checkbox-group">
                  <label
                    v-for="option in companyChallengeOptions"
                    :key="option"
                    class="checkbox-item"
                  >
                    <input
                      type="checkbox"
                      :value="option"
                      v-model="form.companyChallenges"
                    />
                    <span>{{ option }}</span>
                  </label>
                </div>
              </div>

              <div class="challenge-col">
                <label class="form-label-custom">Track Challenges</label>
                <div class="checkbox-group">
                  <label
                    v-for="option in trackChallengeOptions"
                    :key="option"
                    class="checkbox-item"
                  >
                    <input
                      type="checkbox"
                      :value="option"
                      v-model="form.trackChallenges"
                    />
                    <span>{{ option }}</span>
                  </label>
                </div>
              </div>

              <div class="challenge-col">
                <label class="form-label-custom">MLH Challenges</label>
                <div class="checkbox-group">
                  <label
                    v-for="option in mlhChallengeOptions"
                    :key="option"
                    class="checkbox-item"
                  >
                    <input
                      type="checkbox"
                      :value="option"
                      v-model="form.mlhChallenges"
                    />
                    <span>{{ option }}</span>
                  </label>
                </div>
              </div>
            </div>

            <div class="btn-row">
              <button
                type="button"
                class="btn-secondary-custom"
                @click="prevStep"
              >
                Previous
              </button>
              <button type="submit" class="btn-primary-custom">
                {{ submitting ? "Submitting..." : "Submit" }}
              </button>
            </div>
          </fieldset>
        </form>
      </div>
    </div>
  </b-modal>
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
  background-color: transparent;
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
  box-shadow: 0 6px 16px black !important;
}

.submit-btn:active {
  /* transform: translateY(2px) scale(0.97); */
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

/* Modal */
:deep(.submit-modal .modal-content) {
  background-color: #ebebeb;
  border: none;
  border-radius: 1rem;
}

:deep(.modal-body-custom) {
  padding: 1.75rem 2rem;
}

.modal-inner {
  color: #1a1a1a;
}

.warning-banner {
  background-color: #fff3cd;
  border: 1px solid #ffcb3d;
  border-radius: 0.5rem;
  padding: 0.6rem 0.85rem;
  margin-bottom: 1.25rem;
  font-family: var(--font-aleo), serif;
  font-size: 0.8rem;
  font-weight: 600;
  color: #664d03;
  text-align: center;
}

.step-content {
  display: flex;
  flex-direction: column;
}

/* Step header */
.step-header {
  text-align: center;
  margin-bottom: 1.25rem;
}

.step-badge {
  display: inline-block;
  font-family: var(--font-aleo), serif;
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: #fff;
  background: var(--color-bitcamp);
  padding: 0.2rem 0.7rem;
  border-radius: 999px;
  margin-bottom: 0.5rem;
}

.step-title {
  font-family: var(--font-aleo), serif;
  font-size: 1.5rem;
  font-weight: 700;
  color: #1a1a1a;
  margin: 0.25rem 0 0.15rem;
}

.step-subtitle {
  font-family: var(--font-aleo), serif;
  font-size: 0.9rem;
  color: #555;
  margin: 0;
}

/* Devpost step */
.devpost-area {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  margin: 1.5rem 0;
}

.devpost-btn {
  padding: 0.6rem 2rem !important;
  font-size: 1rem !important;
  font-weight: 600 !important;
  font-family: var(--font-aleo), serif;
  border: 2px solid var(--color-bitcamp) !important;
  border-radius: 0.5rem !important;
  background: transparent !important;
  color: var(--color-bitcamp) !important;
  cursor: pointer;
  transition: all 0.15s ease;
}

.devpost-btn:hover {
  background: var(--color-bitcamp) !important;
  color: #fff !important;
}

.devpost-check {
  font-family: var(--font-aleo), serif;
  font-size: 0.85rem;
  font-weight: 600;
  color: #2e7d32;
}

/* Button row */
.btn-row {
  display: flex;
  justify-content: flex-end;
  gap: 0.6rem;
  margin-top: 1.25rem;
  padding-top: 1rem;
  border-top: 1px solid #ddd;
}

.btn-primary-custom {
  padding: 0.5rem 1.75rem;
  font-size: 0.9rem;
  font-weight: 600;
  font-family: var(--font-aleo), serif;
  border: none;
  border-radius: 0.5rem;
  background: linear-gradient(135deg, var(--color-bitcamp), var(--color-flame));
  color: #fff;
  cursor: pointer;
  transition: all 0.15s ease;
}

.btn-primary-custom:disabled {
  opacity: 0.35;
  cursor: not-allowed;
}

.btn-primary-custom:not(:disabled):hover {
  box-shadow: 0 3px 10px rgba(0, 0, 0, 0.2);
}

.btn-secondary-custom {
  padding: 0.5rem 1.75rem;
  font-size: 0.9rem;
  font-weight: 600;
  font-family: var(--font-aleo), serif;
  border: 1px solid #bbb;
  border-radius: 0.5rem;
  background: transparent;
  color: #444;
  cursor: pointer;
  transition: all 0.15s ease;
}

.btn-secondary-custom:hover {
  background: #ddd;
}

/* Form */
.form-area {
  text-align: left;
}

.form-area fieldset {
  border: none;
  margin: 0;
  padding: 0;
}

.form-area fieldset:disabled {
  opacity: 0.5;
  pointer-events: none;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0.75rem;
  margin-bottom: 0.75rem;
}

.form-group-custom {
  margin-bottom: 0.75rem;
}

.form-label-custom {
  display: block;
  font-family: var(--font-aleo), serif;
  font-weight: 600;
  font-size: 0.8rem;
  color: #333;
  margin-bottom: 0.25rem;
}

.form-input-custom {
  width: 100%;
  padding: 0.45rem 0.7rem;
  font-family: var(--font-aleo), serif;
  font-size: 0.85rem;
  color: #1a1a1a;
  background-color: #fff;
  border: 1px solid #ccc;
  border-radius: 0.4rem;
  outline: none;
  transition: border-color 0.15s ease;
}

.form-input-custom::placeholder {
  color: #999;
}

.form-input-custom:focus {
  border-color: var(--color-bitcamp);
}

/* Challenges grid */
.challenges-grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 0.75rem;
  margin-bottom: 0.25rem;
}

.checkbox-group {
  display: flex;
  flex-direction: column;
  gap: 0.3rem;
}

.checkbox-item {
  display: flex;
  align-items: center;
  gap: 0.35rem;
  font-family: var(--font-aleo), serif;
  font-size: 0.8rem;
  color: #1a1a1a;
  cursor: pointer;
}

.checkbox-item input[type="checkbox"] {
  width: 0.85rem;
  height: 0.85rem;
  accent-color: var(--color-bitcamp);
  cursor: pointer;
}
</style>

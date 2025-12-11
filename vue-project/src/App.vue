<template>
  <div class="app-wrapper">
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-md-8 col-lg-6">
          <div class="card-box">
            <div class="text-center mb-4">
              <h1 class="app-title">Parfüm Hesaplayıcı</h1>
              <p class="app-subtitle">
                Mükemmel karışım oranlarını saniyeler içinde bulun.
              </p>
            </div>

            <div class="form-container">
              <form @submit.prevent="calculateResult">
                <div class="mb-4">
                  <label for="totalVolume" class="form-label">Toplam Hacim (ml)</label>
                  <input
                    v-model.number="totalVolume"
                    type="number"
                    class="form-control custom-input"
                    id="totalVolume"
                    placeholder="Örn: 50"
                  />
                </div>
                
                <div class="mb-4">
                  <label for="essencePercentage" class="form-label">Esans Yüzdesi (%)</label>
                  <input
                    v-model.number="essencePercentage"
                    type="number"
                    class="form-control custom-input"
                    id="essencePercentage"
                    placeholder="Örn: 20"
                  />
                </div>

                <div class="mb-4">
                  <label for="essenceChooser" class="form-label">Parfüm Esansı</label>
                  <div class="select-wrapper">
                    <select
                      v-model="selectedEssence"
                      class="form-select custom-input"
                      id="essenceChooser"
                    >
                      <option disabled value="">Bir esans seçiniz</option>
                      <option
                        v-for="essence in essenceList"
                        :key="essence.id"
                        :value="essence"
                      >
                        {{ essence.name }}
                      </option>
                    </select>
                  </div>
                </div>

                <button type="submit" class="btn btn-primary custom-btn w-100">
                  HESAPLA
                </button>
              </form>
            </div>

            <div class="result-section mt-4" v-if="result > 0">
              <div class="result-card">
                <h5 class="result-title">Sonuçlar</h5>
                <div class="result-item" v-if="selectedEssence">
                  <span>Seçim:</span>
                  <span class="value">{{ selectedEssence.name }}</span>
                </div>
                <div class="result-item">
                  <span>Gereken Esans:</span>
                  <span class="value highlight">{{ result }} ml</span>
                </div>
                <div class="result-item">
                  <span>Gereken Çözücü:</span>
                  <span class="value">{{ totalVolume - result }} ml</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      totalVolume: null,
      essencePercentage: null,
      selectedEssence: "",
      result: 0,
      essenceList: [
        { id: 1, name: "Dior Sauvage", price: 100 },
        { id: 2, name: "Mancera Red Tobacco", price: 120 },
        { id: 3, name: "Chanel Bleu", price: 150 },
        { id: 4, name: "Tom Ford Noir", price: 180 },
        { id: 5, name: "Creed Aventus", price: 200 },
      ],
    };
  },
  methods: {
    calculateResult() {
      if (this.totalVolume && this.essencePercentage) {
        this.result = (this.totalVolume * this.essencePercentage) / 100;
      } else {
        alert("Lütfen hacim ve yüzde değerlerini giriniz.");
      }
    },
  },
};
</script>

<style scoped>
.app-wrapper {
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding: 20px 0;
}

.card-box {
  background: #ffffff;
  border-radius: 20px;
  padding: 40px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.app-title {
  font-weight: 700;
  color: #2c3e50;
  font-size: 2rem;
  margin-bottom: 0.5rem;
}

.app-subtitle {
  color: #7f8c8d;
  font-size: 0.95rem;
}

.form-label {
  font-weight: 600;
  color: #34495e;
  font-size: 0.9rem;
  margin-bottom: 8px;
}

.custom-input {
  border: 2px solid #ecf0f1;
  border-radius: 12px;
  padding: 12px 15px;
  font-size: 1rem;
  transition: all 0.3s;
  background-color: #f9fbfd;
}

.custom-input:focus {
  border-color: #3498db;
  box-shadow: 0 0 0 4px rgba(52, 152, 219, 0.1);
  background-color: #fff;
}

.custom-btn {
  background: linear-gradient(45deg, #3498db, #2980b9);
  border: none;
  border-radius: 12px;
  padding: 14px;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
  transition: all 0.3s;
  box-shadow: 0 4px 15px rgba(52, 152, 219, 0.3);
}

.custom-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(52, 152, 219, 0.4);
  background: linear-gradient(45deg, #2980b9, #3498db);
}

.result-card {
  background: #f0fdf4;
  border: 1px solid #dcfce7;
  border-radius: 15px;
  padding: 20px;
  animation: fadeIn 0.5s ease-in-out;
}

.result-title {
  color: #166534;
  font-weight: 700;
  margin-bottom: 15px;
  border-bottom: 1px solid #bbf7d0;
  padding-bottom: 10px;
}

.result-item {
  display: flex;
  justify-content: space-between;
  margin-bottom: 8px;
  font-size: 1rem;
  color: #14532d;
}

.result-item .value {
  font-weight: 600;
}

.result-item .value.highlight {
  color: #15803d;
  font-size: 1.1rem;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
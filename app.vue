<template>
  <section class="profile-page">
    <div class="container">
      <!-- Foto Profil -->
      <div class="profile-section">
        <div class="profile-image">
          <img src="./images/Foto Jas Putih.PNG" alt="Profile Picture" />
        </div>
        <h1>{{ name }}</h1>
        <p>{{ bio }}</p>
      </div>

      <!-- Burger Button for Mobile -->
      <div class="burger-button" @click="toggleMenu">
        <i class="fas" :class="menuVisible ? 'fa-times' : 'fa-bars'"></i>
      </div>

      <!-- Card Sections -->
      <div class="cards-section" v-if="menuVisible || !isMobile">
        <!-- Skills -->
        <div class="card skills-card">
          <div class="card-header">
            <i class="fas fa-code"></i>
            <h2>Skills</h2>
          </div>
          <div v-for="skill in skills" :key="skill.name" class="skill-bar">
            <span>{{ skill.name }}</span>
            <div class="progress">
              <div class="progress-bar" :style="{ width: skill.level + '%' }"></div>
            </div>
          </div>
        </div>

        <!-- Experience -->
        <div class="card experience-card">
          <div class="card-header">
            <i class="fas fa-briefcase"></i>
            <h2>Pengalaman</h2>
          </div>
          <ul>
            <li v-for="experience in experiences" :key="experience.company">
              <strong>{{ experience.position }}</strong> - {{ experience.company }} ({{ experience.year }})
            </li>
          </ul>
        </div>

        <!-- Pendidikan -->
        <div class="card education-card">
          <div class="card-header">
            <i class="fas fa-graduation-cap"></i>
            <h2>Riwayat Pendidikan</h2>
          </div>
          <ul>
            <li v-for="education in educationHistory" :key="education.school">
              <strong>{{ education.degree }}</strong> - {{ education.school }} ({{ education.year }})
            </li>
          </ul>
        </div>
      </div>

      <!-- Contact Me Section -->
      <div class="contact-section">
        <h2>Contact Me</h2>
        <form @submit.prevent="sendMessage">
          <div class="form-group">
            <label for="name">Your Name</label>
            <input type="text" id="name" v-model="form.name" required />
          </div>
          <div class="form-group">
            <label for="email">Your Email</label>
            <input type="email" id="email" v-model="form.email" required />
          </div>
          <div class="form-group">
            <label for="message">Message</label>
            <textarea id="message" v-model="form.message" required></textarea>
          </div>
          <button type="submit" class="submit-btn">Send Message</button>
        </form>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      name: 'Femas Alfaridzi',
      bio: 'Web Developer passionate about creating interactive applications and experiences on the web.',
      skills: [
        { name: 'JavaScript', level: 90 },
        { name: 'Vue.js', level: 85 },
        { name: 'Nuxt.js', level: 80 },
        { name: 'HTML', level: 95 },
        { name: 'CSS', level: 90 }
      ],
      experiences: [
        { position: 'Frontend Developer', company: 'Tech Company', year: '2020-2022' },
        { position: 'Backend Developer', company: 'Software Solutions', year: '2018-2020' }
      ],
      educationHistory: [
        { degree: 'Sarjana Teknologi Informasi', school: 'Universitas Brawijaya', year: '2014-2018' }
      ],
      menuVisible: false,
      isMobile: false,
      form: {
        name: '',
        email: '',
        message: ''
      }
    };
  },
  mounted() {
    this.checkMobile();
    window.addEventListener('resize', this.checkMobile);
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.checkMobile);
  },
  methods: {
    toggleMenu() {
      this.menuVisible = !this.menuVisible;
    },
    checkMobile() {
      this.isMobile = window.innerWidth <= 768;
    },
    sendMessage() {
      alert(`Message sent by ${this.form.name} (${this.form.email}):\n\n${this.form.message}`);
      this.form.name = '';
      this.form.email = '';
      this.form.message = '';
    }
  }
};
</script>

<style>
/* Style for the burger button */
.burger-button {
  display: none;
  cursor: pointer;
  font-size: 2em;
  position: absolute;
  top: 20px;
  right: 20px;
  z-index: 1000;
  color: #fff;
}

.burger-button i {
  font-size: 1.5em;
}

@media (max-width: 768px) {
  .burger-button {
    display: block;
  }

  .cards-section {
    display: none;
  }

  .cards-section.v-if {
    display: block;
  }
}

/* Style other elements */
.profile-page {
  padding: 50px 0;
  background: linear-gradient(135deg, #4a90e2 0%, #007aff 50%, #00c6ff 100%);
  text-align: center;
  position: relative;
}

.container {
  max-width: 1000px;
  margin: 0 auto;
}

.profile-section {
  margin-bottom: 40px;
}

.profile-image {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  overflow: hidden;
  margin: 0 auto 20px;
  border: 5px solid #fff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.profile-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

h1 {
  font-size: 2.5em;
  color: #fff;
  margin-bottom: 10px;
}

p {
  font-size: 1.3em;
  color: #d0eaff;
}

.cards-section {
  display: flex;
  justify-content: space-between;
  gap: 20px;
}

.card {
  background-color: #fff;
  border-radius: 12px;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
  padding: 25px;
  flex: 1;
  text-align: left;
  transition: transform 0.3s ease;
}

.card:hover {
  transform: translateY(-10px);
}

.card-header {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.card-header i {
  font-size: 1.5em;
  color: #4a90e2;
  margin-right: 10px;
}

.card h2 {
  font-size: 1.7em;
  margin: 0;
  color: #333;
}

/* Contact Me Styles */
.contact-section {
  margin-top: 50px;
  background-color: #fff;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
}

.contact-section h2 {
  font-size: 2em;
  margin-bottom: 20px;
  color: #333;
}

.contact-section form {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-group label {
  font-size: 1.2em;
  margin-bottom: 10px;
  color: #333;
}

.form-group input, .form-group textarea {
  padding: 10px;
  font-size: 1.1em;
  border: 2px solid #ccc;
}

.submit-btn {
  background-color: #4a90e2;
  color: #fff;
  padding: 10px 20px;
  font-size: 1.2em;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.submit-btn:hover {
  background-color: #007aff;
}

</style>

<template>
  <div class="app-container">
    <header class="site-header">
      <div class="header-content">
        <h1 class="site-title">Kids Connect</h1>
      </div>
    </header>
    
    <div class="page-container">
      <!-- Левая колонка -->
      <div class="main-content">
        <!-- Поиск и фильтры -->
        <div class="search-filters">
          <div class="search-header">
            <div class="search-wrapper">
              <input type="text" class="search-input" placeholder="Поиск" v-model="searchQuery">
              <button class="map-top-btn" @click="showMap = true">
                <span class="btn-icon">📍</span>
                На карте
              </button>
            </div>
          </div>
          <div class="filter-tabs">
            <button class="filter-tab" :class="{ active: filterType === 'all' }" @click="filterType = 'all'">Все</button>
            <button class="filter-tab" :class="{ active: filterType === 'paid' }" @click="filterType = 'paid'">Платные</button>
            <button class="filter-tab" :class="{ active: filterType === 'free' }" @click="filterType = 'free'">Бесплатные</button>
          </div>
        </div>

        <!-- Силовой спорт -->
        <h2 class="section-title">Силовой спорт</h2>
        <div v-for="(item, index) in filteredSports.filter(s => strengthCategories.includes(s.category.toLowerCase()))" :key="'strength-' + index" class="sport-card">
          <div class="card-image">
            <div class="image-container">
              <img :src="item.image" :alt="item.title" class="sport-image">
              <div class="image-overlay">
                <span class="view-text">Посмотреть</span>
              </div>
            </div>
          </div>
          <div class="card-content-wrapper">
            <div class="card-header">
              <h3 class="sport-title">
                {{ item.title }}
                <span class="sport-subtitle">{{ item.subtitle }}</span>
              </h3>
              <div class="price-tags">
                <span v-if="item.free" class="price-tag free">Бесплатно</span>
                <span v-if="item.firstFree" class="price-tag first-free">Первое бесплатно</span>
                <span v-if="item.price" class="price-tag paid">{{ item.price }}</span>
              </div>
            </div>
            
            <div class="card-content">
              <div class="info-section">
                <div class="info-item">
                  <span class="info-icon">👥</span>
                  <span>{{ item.age }}</span>
                </div>
                <div class="info-item">
                  <span class="info-icon">📍</span>
                  <span>{{ item.address }}</span>
                </div>
                <div class="info-item">
                  <span class="info-icon">🏢</span>
                  <span>{{ item.place }}</span>
                </div>
                <div class="info-item">
                  <span class="info-icon">🕒</span>
                  <span>{{ item.days }}</span>
                  <div class="time-slots">
                    <div v-for="(time, i) in item.times" :key="i" class="time-slot yellow-time">
                      {{ time }}
                    </div>
                  </div>
                </div>
              </div>
              
              <div class="action-buttons">
                <button class="action-btn details-btn" @click="openModal(item)">Подробнее</button>
              </div>
            </div>
          </div>
        </div>

        <!-- Единоборства -->
        <h2 class="section-title">Единоборства</h2>
        <div v-for="(item, index) in filteredSports.filter(s => combatCategories.includes(s.category.toLowerCase()))" :key="'combat-' + index" class="sport-card">
          <div class="card-image">
            <div class="image-container">
              <img :src="item.image" :alt="item.title" class="sport-image">
              <div class="image-overlay">
                <span class="view-text">Посмотреть</span>
              </div>
            </div>
          </div>
          <div class="card-content-wrapper">
            <div class="card-header">
              <h3 class="sport-title">
                {{ item.title }}
                <span class="sport-subtitle">{{ item.subtitle }}</span>
              </h3>
              <div class="price-tags">
                <span v-if="item.free" class="price-tag free">Бесплатно</span>
                <span v-if="item.firstFree" class="price-tag first-free">Первое бесплатно</span>
                <span v-if="item.price" class="price-tag paid">{{ item.price }}</span>
              </div>
            </div>
            
            <div class="card-content">
              <div class="info-section">
                <div class="info-item">
                  <span class="info-icon">👥</span>
                  <span>{{ item.age }}</span>
                </div>
                <div class="info-item">
                  <span class="info-icon">📍</span>
                  <span>{{ item.address }}</span>
                </div>
                <div class="info-item">
                  <span class="info-icon">🏢</span>
                  <span>{{ item.place }}</span>
                </div>
                <div class="info-item">
                  <span class="info-icon">🕒</span>
                  <span>{{ item.days }}</span>
                  <div class="time-slots">
                    <div v-for="(time, i) in item.times" :key="i" class="time-slot yellow-time">
                      {{ time }}
                    </div>
                  </div>
                </div>
              </div>
              
              <div class="action-buttons">
                <button class="action-btn details-btn" @click="openModal(item)">Подробнее</button>
              </div>
            </div>
          </div>
        </div>

        <!-- Гоночный спорт -->
        <h2 class="section-title">Гоночный спорт</h2>
        <div v-for="(item, index) in filteredSports.filter(s => raceCategories.includes(s.category.toLowerCase()))" :key="'race-' + index" class="sport-card">
          <div class="card-image">
            <div class="image-container">
              <img :src="item.image" :alt="item.title" class="sport-image">
              <div class="image-overlay">
                <span class="view-text">Посмотреть</span>
              </div>
            </div>
          </div>
          <div class="card-content-wrapper">
            <div class="card-header">
              <h3 class="sport-title">
                {{ item.title }}
                <span class="sport-subtitle">{{ item.subtitle }}</span>
              </h3>
              <div class="price-tags">
                <span v-if="item.free" class="price-tag free">Бесплатно</span>
                <span v-if="item.firstFree" class="price-tag first-free">Первое бесплатно</span>
                <span v-if="item.price" class="price-tag paid">{{ item.price }}</span>
              </div>
            </div>
            
            <div class="card-content">
              <div class="info-section">
                <div class="info-item">
                  <span class="info-icon">👥</span>
                  <span>{{ item.age }}</span>
                </div>
                <div class="info-item">
                  <span class="info-icon">📍</span>
                  <span>{{ item.address }}</span>
                </div>
                <div class="info-item">
                  <span class="info-icon">🏢</span>
                  <span>{{ item.place }}</span>
                </div>
                <div class="info-item">
                  <span class="info-icon">🕒</span>
                  <span>{{ item.days }}</span>
                  <div class="time-slots">
                    <div v-for="(time, i) in item.times" :key="i" class="time-slot yellow-time">
                      {{ time }}
                    </div>
                  </div>
                </div>
              </div>
              
              <div class="action-buttons">
                <button class="action-btn details-btn" @click="openModal(item)">Подробнее</button>
              </div>
            </div>
          </div>
        </div>

        <!-- Скоростной спорт -->
        <h2 class="section-title">Скоростной спорт</h2>
        <div v-for="(item, index) in filteredSports.filter(s => speedCategories.includes(s.category.toLowerCase()))" :key="'speed-' + index" class="sport-card">
          <div class="card-image">
            <div class="image-container">
              <img :src="item.image" :alt="item.title" class="sport-image">
              <div class="image-overlay">
                <span class="view-text">Посмотреть</span>
              </div>
            </div>
          </div>
          <div class="card-content-wrapper">
            <div class="card-header">
              <h3 class="sport-title">
                {{ item.title }}
                <span class="sport-subtitle">{{ item.subtitle }}</span>
              </h3>
              <div class="price-tags">
                <span v-if="item.free" class="price-tag free">Бесплатно</span>
                <span v-if="item.firstFree" class="price-tag first-free">Первое бесплатно</span>
                <span v-if="item.price" class="price-tag paid">{{ item.price }}</span>
              </div>
            </div>
            
            <div class="card-content">
              <div class="info-section">
                <div class="info-item">
                  <span class="info-icon">👥</span>
                  <span>{{ item.age }}</span>
                </div>
                <div class="info-item">
                  <span class="info-icon">📍</span>
                  <span>{{ item.address }}</span>
                </div>
                <div class="info-item">
                  <span class="info-icon">🏢</span>
                  <span>{{ item.place }}</span>
                </div>
                <div class="info-item">
                  <span class="info-icon">🕒</span>
                  <span>{{ item.days }}</span>
                  <div class="time-slots">
                    <div v-for="(time, i) in item.times" :key="i" class="time-slot yellow-time">
                      {{ time }}
                    </div>
                  </div>
                </div>
              </div>
              
              <div class="action-buttons">
                <button class="action-btn details-btn" @click="openModal(item)">Подробнее</button>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Правая колонка -->
      <aside class="sidebar">
        <div class="filters-section">
          <h3 class="filters-title">Фильтры</h3>
          
          <div class="filter-group">
            <label class="filter-label">Возраст</label>
            <select class="filter-select" v-model="selectedAge">
              <option value="">Любой</option>
              <option>10-12</option>
              <option>13-15</option>
              <option>16-18</option>
            </select>
          </div>

          <div class="filter-group">
            <label class="filter-label">Пол</label>
            <div class="checkbox-group">
              <label class="checkbox-label">
                <input type="checkbox" v-model="filters.male">
                Мужской
              </label>
              <label class="checkbox-label">
                <input type="checkbox" v-model="filters.female">
                Женский
              </label>
            </div>
          </div>

          <div class="catalog-section">
            <h4 class="catalog-title">Каталог</h4>
            <div class="catalog-list">
              <div v-for="(category, index) in catalog" :key="index" class="catalog-item">
                <div class="category-header" @click="toggleCategory(category)">
                  <span class="category-arrow" :class="{ open: category.open }">›</span>
                  <span class="category-name">{{ category.name }}</span>
                  <span class="category-count">{{ category.count }}</span>
                </div>
                
                <div v-if="category.open" class="subcategories">
                  <div v-for="(subcategory, subIndex) in category.subcategories" :key="subIndex" class="subcategory">
                    <span class="subcategory-name">- {{ subcategory.name }}</span>
                    <span class="subcategory-count">{{ subcategory.count }}</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </aside>
    </div>

    <!-- Модальное окно -->
<div v-if="showModal && selectedItem" class="modal-overlay" @click.self="closeModal">
  <div class="modal-content">
    
    <!-- ШАПКА -->
    <div class="modal-header">
      <button class="back-btn" @click="closeModal">← Назад</button>
      <h2 class="modal-title">KidsConnect</h2>
      <button class="map-btn" @click="showMap = true">📍 На карте</button>
    </div>

    <!-- КАРТОЧКА -->
    <div class="modal-card">
      <div class="card-left">
        <img :src="selectedItem.image" :alt="selectedItem.title" class="sport-image">
      </div>
      <div class="card-right">
        <h3 class="sport-title">{{ selectedItem.title }}</h3>
        
        <div class="info-list">
          <p>👥 {{ selectedItem.age }}</p>
          <p>📍 {{ selectedItem.address }}</p>
          <p>🏢 {{ selectedItem.place }}</p>
        </div>

        <div class="status-row">
          <span class="status-open">Набор открыт</span>
          <span v-if="selectedItem.free" class="price-tag free">Бесплатно</span>
        </div>

        <button class="enroll-btn">Записаться</button>
      </div>
    </div>

    <!-- ГРУППЫ и РАСПИСАНИЕ -->
    <div class="groups-schedule">
      <div class="section">
        <h3 class="section-title">ГРУППЫ</h3>
        <p>Этап начальной подготовки</p>
        <p>Петрова Елена Александровна</p>
        <p>15 из 20</p>
        <p>12 месяцев</p>
      </div>
      <div class="section">
        <h3 class="section-title">РАСПИСАНИЕ ЗАНЯТИЙ</h3>
        <p>{{ selectedItem.days }}</p>
        <div class="time-slots">
          <div v-for="(time, i) in selectedItem.times" :key="i" class="time-slot">
            {{ time }}
          </div>
        </div>
      </div>
    </div>

    <!-- ОПИСАНИЕ -->
    <div class="section">
      <h3 class="section-title">ОПИСАНИЕ</h3>
      <p>
        Лёгкая атлетика – олимпийский вид спорта, объединяющий беговые виды,
        спортивную ходьбу, прыжки, метания, многоборья, пробеги и кроссы.
      </p>
    </div>

    <!-- СОДЕРЖАНИЕ ПРОГРАММЫ -->
    <div class="section">
      <h3 class="section-title">СОДЕРЖАНИЕ ПРОГРАММЫ</h3>
      <details>
        <summary>Базовый уровень</summary>
        <p>Первый–второй год обучения – 252 часа.</p>
        <p>Обязательные предметы области (количество часов – 15);</p>
        <p>Вариативные предметные области (количество часов −10);</p>
        <p>Теория (количество часов −5);</p>
        <p>Практика (количество часов − 216);</p>
      </details>
      <details>
        <summary>Углублённый уровень</summary>
        <p>Третий–четвёртый год обучения – 416 часов.</p>
        <p>Обязательные предметы области (количество часов − 27);</p>
        <p>Вариативные предметные области (количество часов − 15);</p>
      </details>
    </div>
  </div>
</div>


    <!-- Модальное окно карты -->
    <div v-if="showMap" class="modal-overlay" @click.self="showMap = false">
      <div class="modal-content map-modal">
        <div class="modal-header">
          <button class="back-btn" @click="showMap = false">
            <span class="back-text">Назад</span>
          </button>
          <h2 class="modal-title">Карта</h2>
        </div>
        <div class="map-container">
          <iframe 
            src="https://yandex.ru/map-widget/v1/?um=constructor%3A0c4c388e3d6d9b1b0b0b0b0b0b0b0b0b0b0&amp;source=constructor" 
            width="100%" 
            height="100%" 
            frameborder="0"
          ></iframe>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, reactive } from 'vue'

const strengthCategories = ['тяжелая атлетика', 'пауэрлифтинг', 'армреслинг']
const combatCategories = ['дзюдо', 'вольная борьба', 'каратэ', 'бокс']
const raceCategories = ['картинг', 'мотокросс']
const speedCategories = ['бег', 'велоспорт']

const sports = [
  { 
    title: 'Тяжелая атлетика', 
    subtitle: '(в Юбилейном мкр.)', 
    category: 'тяжелая атлетика', 
    age: '10-18 лет', 
    address: 'г. Иркутск, Юбилейный мкр., стр. 49/1', 
    place: 'ФОК "Юбилейный"', 
    days: 'Пн, Ср, Пт', 
    times: ['09:00 - 10:30', '12:00 - 13:30', '18:00 - 19:30'], 
    free: true,
    image: 'https://images.unsplash.com/photo-1517344884509-a0c97ec11bcc?w=400&h=300&fit=crop'
  },
  { 
    title: 'Тяжелая атлетика', 
    subtitle: '(на ул. Боткина)', 
    category: 'тяжелая атлетика', 
    age: '10-18 лет', 
    address: 'г. Иркутск, ул. Боткина, 15', 
    place: 'СК "Атлет"', 
    days: 'Вт, Ср, Пт', 
    times: ['09:00 - 10:30', '12:00 - 13:30', '12:00 - 13:30'], 
    firstFree: true, 
    price: '500 руб.',
    image: 'https://avatars.mds.yandex.net/i?id=e6d896541dabde2b5d33123bddad71c5_l-10555703-images-thumbs&n=13'
  },
  { 
    title: 'армреслинг', 
    subtitle: '(в Юбилейном мкр.)', 
    category: 'армреслинг', 
    age: '10-18 лет', 
    address: 'г. Иркутск, Юбилейный мкр., стр. 49/1', 
    place: 'ФОК "Юбилейный"', 
    days: 'Пн, Ср, Пт', 
    times: ['09:00 - 10:30', '12:00 - 13:30', '18:00 - 19:30'], 
    free: true,
    image: 'https://avatars.dzeninfra.ru/get-zen_doc/5192222/pub_61655fb3ddb9d84dfacfe1f9_6174f43b34d7663dc5be99c9/scale_1200'
  },
  { 
    title: 'Дзюдо', 
    subtitle: '', 
    category: 'дзюдо', 
    age: '6–18 лет', 
    address: 'г. Иркутск, ул Трудовая, д 115А', 
    place: 'СК "Рингспец"', 
    days: 'Пн, Ср, Пт', 
    times: ['09:00 - 10:30', '12:00 - 13:30'], 
    free: true,
    image: 'https://avatars.mds.yandex.net/i?id=73138428ac1818640d7c377e1aa07d75_l-13080820-images-thumbs&n=13'
  },
  { 
    title: 'Каратэ', 
    subtitle: '', 
    category: 'каратэ', 
    age: '8–16 лет', 
    address: 'г. Иркутск, ул Спортивная, 22', 
    place: 'ДЮСШ "Спарта"', 
    days: 'Вт, Чт, Пт',  
    times: ['17:00 - 18:30','12:00 - 13:30','12:00 - 13:30'], 
    price: '1000 руб.', 
    firstFree: true,
    image: 'https://i.pinimg.com/originals/82/44/a5/8244a58a119e950a601c1d3f59dab121.jpg'
  },
  { 
    title: 'Бокс', 
    subtitle: '', 
    category: 'бокс', 
    age: '12–18 лет', 
    address: 'г. Иркутск, ул Ленина, 9', 
    place: 'СК "Чемпион"', 
    days: 'Пн, Ср, Пт', 
    times: ['16:00 - 17:30','12:00 - 13:30','12:00 - 13:30'], 
    free: true,
    image: 'https://i.pinimg.com/originals/f7/82/e8/f782e8c3b24b22a6beaee4eec7effc20.jpg'
  },
  { 
    title: 'Картинг', 
    subtitle: '', 
    category: 'картинг', 
    age: '10–17 лет', 
    address: 'г. Иркутск, ул Дорожная, 30', 
    place: 'Автодром Юниор', 
    days: 'Сб, Вс, Пн', 
    times: ['11:00 - 13:00','12:00 - 13:30','12:00 - 13:30'], 
    price: '1500 руб.',
    image: 'https://avatars.mds.yandex.net/i?id=a45fdd415994593f852e15d4a49b28bf_l-9820447-images-thumbs&n=13'
  },
  { 
    title: 'Мотокросс', 
    subtitle: '', 
    category: 'мотокросс', 
    age: '12–18 лет', 
    address: 'г. Иркутск, ул Окружная, 9', 
    place: 'Трасса "Вихрь"', 
    days: 'Сб, Пн, Вт', 
    times: ['14:00 - 16:00','12:00 - 13:30','12:00 - 13:30'], 
    firstFree: true,
    image: 'https://avatars.mds.yandex.net/i?id=9126540263c8f5d47093c8517e73a389_l-4936279-images-thumbs&n=13'
  },
  { 
    title: 'Бег 100м', 
    subtitle: '', 
    category: 'бег', 
    age: '10–16 лет', 
    address: 'г. Иркутск, ул Ленина, 2', 
    place: 'Стадион "Центральный"', 
    days: 'Вт, Чт, Пн', 
    times: ['17:00 - 18:30','12:00 - 13:30','12:00 - 13:30'], 
    free: true,
    image: 'https://images.unsplash.com/photo-1552674605-db6ffd4facb5?w=400&h=300&fit=crop'
  },
  { 
    title: 'Велоспорт', 
    subtitle: '', 
    category: 'велоспорт', 
    age: '10–17 лет', 
    address: 'г. Иркутск, ул Байкальская, 45', 
    place: 'Спортпарк "Байкал"', 
    days: 'Ср, Пт, Пн', 
    times: ['10:00 - 11:30', '12:00 - 13:30', '12:00 - 13:30'], 
    price: '800 руб.',
    image: 'https://i.pinimg.com/originals/60/a1/b8/60a1b83889e5f380824330aa284898e0.jpg'
  }
]

// Состояния для фильтров
const searchQuery = ref('')
const filterType = ref('all')
const selectedAge = ref('')
const filters = reactive({
  male: true,
  female: true
})
const showMap = ref(false)

// Каталог с подкатегориями
const catalog = ref([
  {
    name: 'Силовой спорт',
    count: 3,
    open: false,
    subcategories: [
      { name: 'Тяжелая атлетика', count: 3 },
      { name: 'Пауэрлифтинг', count: 1 }
    ]
  },
  {
    name: 'Единоборства',
    count: 2,
    open: false,
    subcategories: [
      { name: 'Вольная борьба', count: 1 },
      { name: 'Дзюдо', count: 1 }
    ]
  },
  {
    name: 'Гоночный спорт',
    count: 0,
    open: false,
    subcategories: [
      { name: 'Картинг', count: 0 },
      { name: 'Мотокросс', count: 0 }
    ]
  },
  {
    name: 'Скоростной спорт',
    count: 0,
    open: false,
    subcategories: [
      { name: 'Бег 100м', count: 0 },
      { name: 'Велоспорт', count: 0 }
    ]
  }
])

const filteredSports = computed(() => {
  return sports.filter(item => {
    const matchesSearch = item.title.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
                         item.subtitle.toLowerCase().includes(searchQuery.value.toLowerCase())
    
    const matchesFilter = filterType.value === 'all' ||
                         (filterType.value === 'free' && item.free) ||
                         (filterType.value === 'paid' && !item.free)
    
    return matchesSearch && matchesFilter
  })
})

const selectedItem = ref(null)
const showModal = ref(false)

function openModal(item) {
  selectedItem.value = item
  showModal.value = true
}

function closeModal() {
  showModal.value = false
}

function toggleCategory(category) {
  category.open = !category.open
}
</script>


<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Roboto', 'Arial', sans-serif;
  background-color: #f0f0f0;
  color: #333;
  line-height: 1.4;
}

.app-container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  width: 100%;
  background-color: #f0f0f0;
}

.site-header {
  background: linear-gradient(135deg, #7d0c25 0%, #a3162f 100%);
  color: white;
  padding: 20px 0;
  text-align: center;
  margin-bottom: 24px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  position: sticky;
  top: 0;
  z-index: 100;
  width: 100%;
}

.header-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 16px;
}

.site-title {
  font-size: 32px;
  font-weight: 700;
  letter-spacing: 0.5px;
}

.page-container {
  display: flex;
  max-width: 1200px;
  margin: 0 auto;
  gap: 24px;
  padding: 0 16px;
  flex: 1;
  width: 100%;
}

.main-content {
  flex: 1;
  min-width: 0;
}

.search-filters {
  background: white;
  padding: 20px;
  border-radius: 12px;
  margin-bottom: 24px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.05);
}

.search-header {
  display: flex;
  align-items: center;
  gap: 16px;
  margin-bottom: 16px;
}

.search-wrapper {
  flex: 1;
  display: flex;
  gap: 12px;
  align-items: center;
}

.search-input {
  flex: 1;
  padding: 12px 16px;
  border: 2px solid #e9ecef;
  border-radius: 8px;
  font-size: 14px;
  transition: border-color 0.2s;
}

.search-input:focus {
  outline: none;
  border-color: #7d0c25;
}

.map-top-btn {
  padding: 12px 20px;
  background: #7d0c25;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  transition: background 0.2s;
  white-space: nowrap;
  display: flex;
  align-items: center;
  gap: 6px;
}

.map-top-btn:hover {
  background: #a3162f;
}

.btn-icon {
  font-size: 16px;
}

.filter-tabs {
  display: flex;
  gap: 8px;
}

.filter-tab {
  padding: 8px 16px;
  border: 2px solid #e9ecef;
  border-radius: 20px;
  background: white;
  color: #666;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
}

.filter-tab:hover {
  border-color: #7d0c25;
  color: #7d0c25;
}

.filter-tab.active {
  background: #7d0c25;
  border-color: #7d0c25;
  color: white;
}

.section-title {
  font-size: 20px;
  font-weight: 600;
  color: #7d0c25;
  margin: 24px 0 16px 0;
  padding-bottom: 8px;
  border-bottom: 2px solid #e9ecef;
}

.sport-card {
  background: white;
  border-radius: 12px;
  margin-bottom: 24px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.05);
  border: 1px solid #e9ecef;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  position: relative;
  overflow: hidden;
  display: flex;
}

.sport-card::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  width: 4px;
  background: #7d0c25;
  border-radius: 2px 0 0 2px;
}

.sport-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

.sport-card:hover::before {
  background: #a3162f;
  width: 5px;
}

.card-image {
  width: 200px;
  height: 200px;
  flex-shrink: 0;
  position: relative;
  margin: 16px;
  border-radius: 8px;
  overflow: hidden;
}

.image-container {
  width: 100%;
  height: 100%;
  position: relative;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transition: transform 0.2s ease;
}

.sport-card:hover .image-container {
  transform: scale(1.05);
}

.sport-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(125, 12, 37, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.2s ease;
}

.sport-card:hover .image-overlay {
  opacity: 1;
}

.view-text {
  color: white;
  font-size: 12px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.card-content-wrapper {
  flex: 1;
  padding: 20px;
  display: flex;
  flex-direction: column;
}

.card-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 12px;
  margin-bottom: 16px;
}

.sport-title {
  font-size: 18px;
  font-weight: 600;
  color: #333;
  margin: 0;
}

.sport-subtitle {
  color: #666;
  font-weight: 400;
  margin-left: 4px;
  font-size: 14px;
}

.card-content {
  display: flex;
  flex-direction: column;
  gap: 16px;
  flex: 1;
}

.info-section {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.info-item {
  display: flex;
  align-items: flex-start;
  gap: 8px;
  font-size: 14px;
  color: #666;
}

.info-item:last-child {
  flex-direction: column;
  align-items: flex-start;
  gap: 8px;
}

.info-icon {
  width: 16px;
  text-align: center;
  flex-shrink: 0;
}

.time-slots {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-top: 4px;
}

.time-slot {
  background: #ffe10087;
  padding: 6px 10px;
  border-radius: 6px;
  font-size: 12px;
  font-weight: 500;
  color: #333;
  border: 1px solid #ffc107;
  white-space: nowrap;
}

.price-tags {
  display: flex;
  gap: 6px;
  flex-wrap: wrap;
  justify-content: flex-end;
}

.price-tag {
  padding: 4px 8px;
  border-radius: 12px;
  font-size: 11px;
  font-weight: 600;
  text-transform: uppercase;
}

.price-tag.free {
  background: #dc3545;
  color: white;
}

.price-tag.first-free {
  background: #007bff;
  color: white;
}

.price-tag.paid {
  background: #dc3545;
  color: white;
}

.action-buttons {
  display: flex;
  justify-content: flex-end;
  margin-top: auto;
}

.action-btn {
  padding: 8px 16px;
  border: none;
  border-radius: 6px;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
}

.details-btn {
  background: #7d0c25;
  color: white;
}

.details-btn:hover {
  background: #a3162f;
}

.sidebar {
  width: 280px;
  flex-shrink: 0;
}

.filters-section {
  background: white;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.05);
}

.filters-title {
  font-size: 18px;
  font-weight: 600;
  color: #7d0c25;
  margin-bottom: 16px;
  padding-bottom: 8px;
  border-bottom: 2px solid #e9ecef;
}

.filter-group {
  margin-bottom: 20px;
}

.filter-label {
  display: block;
  font-size: 14px;
  font-weight: 500;
  color: #333;
  margin-bottom: 8px;
}

.filter-select {
  width: 100%;
  padding: 8px 12px;
  border: 2px solid #e9ecef;
  border-radius: 6px;
  font-size: 14px;
  background: white;
}

.checkbox-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.checkbox-label {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 14px;
  color: #666;
  cursor: pointer;
}

.catalog-section {
  margin-top: 24px;
}

.catalog-title {
  font-size: 16px;
  font-weight: 600;
  color: #333;
  margin-bottom: 12px;
}

.catalog-list {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.category-header {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px 0;
  cursor: pointer;
  user-select: none;
}

.category-arrow {
  font-size: 16px;
  transition: transform 0.2s;
  color: #7d0c25;
}

.category-arrow.open {
  transform: rotate(90deg);
}

.category-name {
  flex: 1;
  font-size: 14px;
  font-weight: 500;
  color: #333;
}

.category-count {
  background: #7d0c25;
  color: white;
  padding: 2px 6px;
  border-radius: 10px;
  font-size: 11px;
  font-weight: 600;
}

.subcategories {
  margin-left: 20px;
  padding: 4px 0;
}

.subcategory {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 4px 0;
}

.subcategory-name {
  flex: 1;
  font-size: 13px;
  color: #666;
}

.subcategory-count {
  background: #6c757d;
  color: white;
  padding: 2px 6px;
  border-radius: 10px;
  font-size: 10px;
  font-weight: 600;
}

/* СТИЛИ ДЛЯ МОДАЛЬНОГО ОКНА */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  padding: 20px;
}

.modal-content {
  background: white;
  border-radius: 12px;
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
  overflow: hidden;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 24px;
  border-bottom: 1px solid #e9ecef;
  background: #f8f9fa;
}

.back-btn {
  background: none;
  border: none;
  color: #7d0c25;
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
  padding: 8px;
  display: flex;
  align-items: center;
}

.back-text {
  margin-left: 4px;
}

.modal-title {
  font-size: 18px;
  font-weight: 700;
  color: #7d0c25;
  margin: 0;
}

.map-btn {
  background: #7d0c25;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 6px;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 6px;
}

.modal-body {
  padding: 24px;
}

.modal-sport-card {
  margin-bottom: 24px;
}

/* Секции групп и расписания ПОД карточкой */
.modal-sections {
  display: flex;
  gap: 24px;
}

.modal-section {
  flex: 1;
  background: #f8f9fa;
  border-radius: 8px;
  padding: 16px;
}

.modal-section-title {
  font-size: 16px;
  font-weight: 700;
  color: #7d0c25;
  margin: 0 0 12px 0;
  padding-bottom: 8px;
  border-bottom: 2px solid #e9ecef;
}

.group-info, .schedule-info {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.group-detail, .schedule-detail {
  font-size: 14px;
  color: #333;
  margin: 0;
  line-height: 1.4;
}

/* Адаптивность для мобильных */
@media (max-width: 1024px) {
  .page-container {
    gap: 16px;
  }
  
  .card-image {
    width: 160px;
    height: 160px;
  }
}

@media (max-width: 768px) {
  .page-container {
    flex-direction: column;
    padding: 0 12px;
  }
  
  .sport-card {
    flex-direction: column;
  }
  
  .card-image {
    width: 100%;
    height: 200px;
    margin: 0;
    border-radius: 12px 12px 0 0;
  }

  .modal-sections {
    flex-direction: column;
  }
  
  .modal-body {
    padding: 16px;
  }
  
  .search-header {
    flex-direction: column;
    align-items: stretch;
  }
  
  .search-wrapper {
    flex-direction: column;
  }
  
  .map-top-btn {
    width: 100%;
    justify-content: center;
  }
}

@media (max-width: 480px) {
  .site-title {
    font-size: 24px;
  }
  
  .section-title {
    font-size: 18px;
  }
  
  .sport-title {
    font-size: 16px;
  }
  
  .modal-overlay {
    padding: 10px;
  }
  
  .modal-content {
    max-width: 100%;
    border-radius: 8px;
  }
  
  .modal-header {
    padding: 12px;
  }
  
  .modal-title {
    font-size: 16px;
  }
  
  .modal-sport-card {
    padding: 12px;
  }
  
  .modal-section {
    padding: 12px;
  }
  
  .card-header {
    flex-direction: column;
    align-items: flex-start;
  }
  
  .price-tags {
    justify-content: flex-start;
  }
  
  .time-slots {
    flex-direction: column;
    align-items: flex-start;
    gap: 4px;
  }
  
  .time-slot {
    width: 100%;
    text-align: center;
  }
  
  .card-image {
    height: 160px;
  }
}


/* === БАЗОВОЕ === */
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.7);
  display: flex;
  justify-content: center;
  align-items: flex-start;
  padding: 20px;
  z-index: 1000;
  overflow-y: auto;
}

.modal-content {
  background: #fff;
  border-radius: 12px;
  max-width: 900px;
  width: 100%;
  box-shadow: 0 8px 30px rgba(0,0,0,0.3);
  overflow: hidden;
  font-family: "Arial", sans-serif;
  color: #444;
}

/* === ШАПКА === */
.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #fff;
  padding: 16px 24px;
  border-bottom: 2px solid #eee;
}
.modal-title {
  color: #7d0c25;
  font-weight: 700;
  font-size: 18px;
}
.back-btn {
  border: none;
  background: none;
  color: #7d0c25;
  font-weight: 600;
  cursor: pointer;
  font-size: 14px;
}
.map-btn {
  background: #7d0c25;
  color: #fff;
  border: none;
  padding: 8px 14px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 14px;
  transition: background 0.2s;
}
.map-btn:hover {
  background: #5e0a1c;
}

/* === КАРТОЧКА === */
.modal-card {
  display: flex;
  padding: 24px;
  gap: 24px;
  border-bottom: 2px solid #eee;
  background: #fff;
}
.card-left img {
  width: 280px;
  height: 200px;
  border-radius: 10px;
  object-fit: cover;
}
.card-right {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}
.sport-title {
  font-size: 20px;
  font-weight: 700;
  margin-bottom: 12px;
  color: #222;
}
.info-list p {
  margin: 4px 0;
  font-size: 14px;
  display: flex;
  align-items: center;
  gap: 6px;
}
.status-row {
  display: flex;
  align-items: center;
  gap: 12px;
  margin: 14px 0;
}
.status-open {
  background: #e8f5e9;
  color: #2e7d32;
  padding: 4px 10px;
  border-radius: 6px;
  font-size: 13px;
  font-weight: 600;
}
.price-tag.free {
  background: #fbe9eb;
  color: #7d0c25;
  padding: 4px 10px;
  border-radius: 6px;
  font-size: 13px;
  font-weight: 600;
}
.enroll-btn {
  margin-top: auto;
  background: #7d0c25;
  color: #fff;
  border: none;
  padding: 10px 20px;
  border-radius: 8px;
  cursor: pointer;
  font-weight: 600;
  transition: background 0.2s;
}
.enroll-btn:hover {
  background: #5e0a1c;
}

/* === ГРУППЫ и РАСПИСАНИЕ === */
.groups-schedule {
  display: flex;
  gap: 20px;
  padding: 20px;
  background: #f8f9fa;
  border-bottom: 2px solid #eee;
}
.groups-schedule .section {
  flex: 1;
  background: #fff;
  border-radius: 8px;
  padding: 16px;
  box-shadow: 0 2px 6px rgba(0,0,0,0.05);
}
.section-title {
  font-weight: 700;
  color: #7d0c25;
  margin-bottom: 10px;
  border-bottom: 1px solid #ddd;
  padding-bottom: 6px;
  font-size: 15px;
}
.time-slots {
  display: flex;
  gap: 6px;
  margin-top: 6px;
  flex-wrap: wrap;
}
.time-slot {
  background: #fff3cd;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 13px;
}

/* === ОБЩИЕ СЕКЦИИ (описание, программа) === */
.section {
  padding: 20px;
  border-top: 2px solid #eee;
}
.section p {
  font-size: 14px;
  line-height: 1.6;
  margin: 6px 0;
}

/* === АККОРДЕОН === */
details {
  margin: 8px 0;
  padding: 10px;
  border: 1px solid #eee;
  border-radius: 6px;
  background: #fafafa;
}
summary {
  cursor: pointer;
  font-weight: 600;
  color: #333;
  position: relative;
  padding-left: 20px;
}
summary::before {
  content: "➤";
  position: absolute;
  left: 0;
  transition: transform 0.2s;
}
details[open] summary::before {
  transform: rotate(90deg);
}

/* === АДАПТИВ === */
@media (max-width: 768px) {
  .modal-card {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }
  .card-left img {
    width: 100%;
    height: 220px;
  }
  .card-right {
    align-items: center;
  }
  .enroll-btn {
    align-self: center;
  }
  .groups-schedule {
    flex-direction: column;
  }
}
@media (max-width: 480px) {
  .modal-content {
    border-radius: 8px;
  }
  .modal-header {
    padding: 12px;
  }
  .modal-card {
    padding: 16px;
  }
  .section {
    padding: 16px;
  }
}



</style>
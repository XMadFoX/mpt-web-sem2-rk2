<template>
  <div class="container">
    <section class="books">
      <h1 class="books__title">Подборка книг для начинающего WEB-программиста</h1>
      <ul class="category-list">
        <li v-for="category in categories">
          <h2 class="category__title">{{ category.title }}</h2>
          <ul class="book-list">
            <li class="book-card" v-for="book in category.books">
              <img class="book-card__cover" :src="book.cover" :alt="book.title">
              <div class="book-card__info">
                <h2 class="book-card__title">
                  {{ book.title }}
                </h2>
                <p>{{ book.description }}</p>
                <p class="book-card__author">{{ book.author }}</p>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </section>
    <section class="reading-section">
      <h2>Список для чтения</h2>
      <ul class="reading-list">
        <li class="reading-card" v-for="card in readingList">
          {{ card.title }}<span @if="card.category.length > 0"> в {{ card.category }}</span>
        </li>
      </ul>
      <p @if="readingList.length === 0">Пусто</p>
      <form @submit="e => addBook(e)" class="add-form">
        <h3>Добавить книгу</h3>
        <input type="text" placeholder="Название книги" v-model="newBook.title" required>
        <div>
          <select v-model="newBook.category">
            <option disabled selected>Выберите категорию</option>
            <option v-for="category in categories" :value="category.title">
              {{ category.title }}
            </option>
          </select>
          <input type="number" min="1" max="5" v-model="newBook.priority">
          <button class="add-form__button" type="submit">Добавить</button>
        </div>
      </form>
    </section>
  </div>
</template>

<style lang="scss">
@use '@/assets/css/main.scss';

.container {
  max-width: 1280px;
  margin: 0 auto;
}

.category-list {
  padding: 0;
}

.category__title {
  text-align: center;
}

.books__title {
  text-align: center;
  margin-top: 2rem;

  @media (min-width: 768px) {
    margin-top: 4rem;
    font-size: 2.5rem;
  }
}

.book-list {
  appearance: none;
  list-style: none;
  display: flex;
  flex-direction: column;
  max-width: 1200px;
  gap: 2rem;
  padding: 1rem;

  @media (min-width: 768px) {
    padding: 2rem;
    margin: 0 auto;
  }
}

.book-card {
  background-color: main.$aqua;
  border-radius: 0.25rem;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  box-shadow: 0 0.25rem 0.5rem rgba(0, 0, 0, 0.25);

  @media (min-width: 768px) {
    flex-direction: row;
    // align-items: center;
    gap: 1rem;
  }

  // flex-direction: row-reverse;
}

.book-card__info {
  padding: 0.5rem;
  display: flex;
  flex-direction: column;
}

.book-card__cover {
  max-width: 200px;
}

.book-card__title {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
}

.book-card__author {
  margin-top: auto;
  font-style: italic;
  font-size: 0.75rem;
  color: main.$primary;
}

.add-form {
  background-color: main.$secondary;
  border-radius: 0.25rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  max-width: 600px;
  margin: 2rem auto;
  appearance: none;
  padding: 1rem;

  &>*:nth-child(3) {
    display: flex;
    flex-direction: column;
    gap: 1rem;

    @media (min-width: 768px) {
      flex-direction: row;
    }


    &>* {
      @media (min-width: 768px) {
        width: 50%;
      }
    }
  }
}

.add-form__button {
  background-color: main.$yellow;
  appearance: none;
  border: none;
  padding: 0.25rem;
  border-radius: 0.25rem;
}

.reading-section {
  text-align: center;
}
</style>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
  data() {
    return {
      categories: [
        {
          title: 'HTML & CSS',
          books: [
            { title: 'HTML и CSS', author: 'Джон Дакетт', description: 'Этот учебник считается одним из лучших на сегодняшний день для изучения описанных выше инструментов веб-программирования. Он прекрасно подходит для начинающих, так как все возможности описываются с нуля и максимально подробно. Много примеров и полезных советов, очень простой язык и подача материала. Для новичков – лучше не придумаешь.', cover: 'https://techrocks.ru/wp-content/uploads/2018/11/kniga-html-i-css-razrabotka-i-dizajn-veb-sajtov-600x800-576x768.jpg' },
            { title: 'HTML5 + CSS3. Основы современного WEB-дизайна', author: 'Джон Дакетт', description: 'Этот учебник также прекрасно подойдет для новичков, так как тоже начинается с самых азов веб-программирования. Книга выпущена в 2018 году, все примеры, задачи, даже синтаксис уже основаны на современных версиях HTML и CSS с учетом их важных особенностей. Книга подойдет как «чайнику», который хочет разобраться в основах работы с сайтами, так и опытным верстальщикам или дизайнерам. Здесь рассматриваются в числе прочего методы создания современных адаптивных дизайнов, работа с визуальными формами и фреймворками, описание визуальных функций CSS3 и т.д. В книге очень много практических примеров.', cover: 'https://techrocks.ru/wp-content/uploads/2018/11/73409.jpg' },
          ]
        },
        {
          title: 'JavaScript',
          books: [
            { title: 'Изучаем программирование на JavaScript', author: 'Эрик Фримен, Элизабет Робсон', description: 'Один из лучших учебников для новичков в веб-программировании. Очень простой язык, удобная подача информации. Новичкам будут особенно интересны базовые возможности, синтаксис и основной функционал. С опытом вы заинтересуетесь, как писать код, одинаково работающий в разных браузерах, как делать JavaScript-код максимально легким и быстрым, избегать проблем с передачей данных, защитить свой ресурс от взлома и т.д. В книге много примеров, практических задач и даже готовых небольших приложений, которые помогут понять на практике, что такое JavaScript.', cover: 'https://techrocks.ru/wp-content/uploads/2018/12/9523650-elizabet-robson-izuchaem-programmirovanie-na-javascript-9523650.jpg' },
            { title: 'JavaScript. Подробное руководство', author: 'Дэвид Флэнаган', description: 'Автор этого учебника – практикующий программист, который постоянно совершенствуется. Сейчас уже вышло 6-е издание, в котором автор обновил некоторые нюансы работы с новыми версиями языка. Это издание не совсем подходит для новичков, так как язык изложения несколько суховат, и основы описаны сжато. Но если вы сначала ознакомитесь с азами и синтаксисом, «Подробное руководство» поможет вам изучить многочисленные нюансы работы в JavaScript. В книге очень много полезных и оригинальных примеров.', cover: 'https://techrocks.ru/wp-content/uploads/2018/12/9523650-elizabet-robson-izuchaem-programmirovanie-na-javascript-9523650.jpg' },
          ]
        },
        {
          title: 'PHP',
          books: [
            { title: 'PHP7 для начинающих с пошаговыми инструкциями', author: 'Майк МакГрат', description: 'Очень простой самоучитель для начинающих. Понятные по-шаговые инструкции, максимум примеров, пояснения на уровне «чайников» — все это позволит познакомиться с этим важнейшим для веб-программирования языком на практике и даже создать собственный сайт.', cover: 'https://techrocks.ru/wp-content/uploads/2018/11/33561224.cover_-529x768.jpg' }
          ]
        }
      ],
      newBook: {
        title: '',
        category: null,
        priority: 1,
      },
      readingList: [] as { title: string, category: string | null, priority: number | null }[]
    }
  },
  methods: {
    addBook(e: any) {
      e.preventDefault();
      this.readingList.push({
        title: this.newBook.title,
        category: this.newBook.category,
        priority: this.newBook.priority,
      })

      // reset current
      this.newBook.title = '';
      this.newBook.category = null;
      this.newBook.priority = 1;

    }
  }
})
</script>

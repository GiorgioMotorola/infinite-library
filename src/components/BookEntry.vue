<template>
  <header>
  <div class="infinite-text">infin<span style="font-weight: bold; color: #C3A6A0;">i</span>telibraryi<span style="font-weight: bold; color: #C3A6A0;">n</span>finitelibraryin<span style="font-weight: bold; color: #C3A6A0;">f</span>initel<span style="font-weight: bold; color: #C3A6A0;">i</span>braryi<span style="font-weight: bold; color: #C3A6A0;">n</span>fin<span style="font-weight: bold; color: #C3A6A0;">i</span>telibraryinfini<span style="font-weight: bold; color: #C3A6A0;">t</span>elibraryinfinit<span style="font-weight: bold; color: #C3A6A0;">e</span>libraryinfinite<span style="font-weight: bold; color: #C3A6A0;">l</span>ibrary<span style="font-weight: bold; color: #C3A6A0;">i</span>nfiniteli<span style="font-weight: bold; color: #C3A6A0;">b</span>raryinfinitelib<span style="font-weight: bold; color: #C3A6A0;">r</span>aryinfinitelibr<span style="font-weight: bold; color: #C3A6A0;">a</span>ryinfinitelibra<span style="font-weight: bold; color: #C3A6A0;">r</span>yinfinitelibrar<span style="font-weight: bold; color: #C3A6A0;">y</span>infinitelibraryinfinitelibraryinfinitelibrary</div>
</header>
  <div class="book-blog-container">
    <div class="total-counts-top-right">
      <p>{{ totalBookCount }} books</p>
      <p>{{ totalPageCount }} pages</p>
      <p>{{ totalWordCount }} words</p>
    </div>
    <div
      class="book-entry"
      v-for="(book, index) in books"
      :key="book.entry"
      :data-entry-number="index + 1" >
      <div class="book-header">
        <img :src="book.image" :alt="book.title" class="book-cover-blog">
        <div class="book-info-header">
          <h2 class="book-title-blog">{{ book.title }}</h2>
          <p class="book-author-blog">{{ book.author }}</p>
          <p class="genre">{{ book.genre }}</p>

          <p class="book-dates-blog">Read between {{ formatDate(book.dateStarted) }} & {{ formatDate(book.dateFinished) }}</p>
          <div v-if="book.ranking" class="book-ranking-blog">
            <span v-for="n in book.ranking" :key="'star-' + n" class="star-blog">★</span>
          </div>
        </div>
      </div>
      <div class="book-content">
        <h3 class="section-title"></h3>
        <p class="book-plot-blog">{{ book.plot }}</p>
        <div v-if="book.thoughts" class="book-thoughts-blog">
          <h3 class="section-title"></h3>
          <p>{{ book.thoughts }}</p>
        </div>
        <hr class="entry-divider">
      </div>
    </div>
  </div>
</template>


<script>
import booksData from '/public/books.json';

export default {
  name: 'BookBlog',
  data() {
    return {
      books: booksData,
    };
  },
  computed: {
    totalPageCount() {
      return this.books.reduce((sum, book) => sum + (book.pageCount || 0), 0);
    },
    totalWordCount() {
      return this.books.reduce((sum, book) => sum + (book.wordCount || 0), 0);
    },
    totalBookCount() {
  return this.books.reduce((latestEntry, book) => {
    return Math.max(latestEntry, book.entry);
  }, 0);
},
  },
  methods: {
    formatDate(dateString) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' };
      return new Date(dateString).toLocaleDateString(undefined, options);
    },
    formatTotalCount(count) {
      if (count >= 1000000) {
        return (count / 1000000).toFixed(1) + 'M';
      } else if (count >= 1000) {
        return (count / 1000).toFixed(0) + 'K';
      }
      return count;
    },
  },
};
</script>

<style scoped>
header {
  white-space: nowrap; 
  overflow: hidden; 
}
.infinite-text {
  font-size: 1.7rem; 
  color: #d8d8d8; 
}
.book-blog-container {
  font-family: "Merriweather", serif;
  color: #262220;
  padding: 2rem;
  max-width: 960px;
  margin: 0 auto;
  position: relative; 
}

.total-counts-top-right {
  text-align: right;
  margin-bottom: 1.5rem;
  color: #262220;
}

.total-counts-top-right p {
  margin: 0.25rem 0;
  font-size: 0.9rem;
}

.book-entry {
  margin-bottom: 2rem;
  padding: 1.5rem;
  border: 2px solid black;
  /* border-radius: 8px; */
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
  position: relative; 
}

.book-entry:before {
  content: attr(data-entry-number); 
  position: absolute;
  top: 10px; 
  right: 10px; 
  font-size: 3rem;
  color: #F7F1F0;
  font-weight: bold;
  background-color: rgba(255, 255, 255, 0.8); 
  padding: 0.2rem 0.4rem;
  border-radius: 4px;
  z-index: 1; 
  -webkit-text-stroke: 1px black;
}

.book-header {
  display: flex;
  align-items: center;
  margin-bottom: 1rem;
  background-color: #fff;
}

.book-cover-blog {
  width: 200px;
  height: auto;
  object-fit: cover;
  /* border-radius: 4px; */
  margin-right: 1.5rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
  border: 3px solid black;
}

.book-info-header {
  flex-grow: 1;
  background-color: #fff;
}

.book-title-blog {
  font-family: "EB Garamond", serif;
  font-size: 2.5rem;
  margin-bottom: 0.3rem;
  color: #262220;
  font-weight: 500;
  background-color: #fff;
}

.book-author-blog {
  font-style: italic;
  color: #928c8c;
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
  background-color: #fff;
}

.book-dates-blog, .genre {
  color: #262220;
  font-size: 0.8rem;
  /* margin-bottom: 0.75rem; */
  background-color: #fff;
}

.book-ranking-blog {
  color: #262220;
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
  background-color: #fff;
}

.star-blog {
  color: rgb(65, 65, 65);
  font-size: 1rem;
  margin-right: 0.2rem;
  background-color: #fff;
}

.book-content {
  padding-top: 1rem;
  background-color: #fff;
}

.section-title {
  font-family: "EB Garamond", serif;
  font-size: 1.3rem;
  color: #262220;
  margin-bottom: 0.75rem;
  border-bottom: 1px solid #e0e0e0;
  padding-bottom: 0.4rem;
  background-color: #fff;
}

.book-plot-blog {
  color: #262220;
  line-height: 1.7;
  font-size: .75rem;
  margin-bottom: 1.25rem;
  font-style: italic;
  background-color: #fff;
}

.book-thoughts-blog {
  margin-top: 1.5rem;
  padding: 1rem;
  border-radius: 4px;
  background-color: #eaf2f35d;
}

.book-thoughts-blog h3.section-title {
  font-size: 0;
  padding-bottom: 0;
  border-bottom: none;
  margin-bottom: 0;
  background-color: #eaf2f35d;
}

.book-thoughts-blog p {
  color: #262220;
  line-height: 1.7;
  font-size: 1rem;
  margin-bottom: 1rem;
  background-color: #eaf2f35d;
}

.entry-divider {
  border: 0;
  border-top: 1px solid #eee;
  margin: 2rem 0 0;
}
</style>
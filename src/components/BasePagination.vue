<template>
  <ul class="catalog__pagination pagination">
    <li class="pagination__item">
      <a class="pagination__link pagination__link--arrow"
         href="#" :class="{'pagination__link--disabled': page == 1}"
         aria-label="Предыдущая страница" @click.prevent="prevPaginate(page)">
        <svg width="8" height="14" fill="currentColor">
          <use xlink:href="#icon-arrow-left"></use>
        </svg>
      </a>
    </li>
    <li class="pagination__item" v-for="pageNumber in pages" :key="pageNumber">
      <a href="#" class="pagination__link"
         :class="{'pagination__link--current' : pageNumber === page}"
         @click.prevent="paginate(pageNumber)">
        {{ pageNumber }}
      </a>
    </li>
    <li class="pagination__item">
      <a class="pagination__link pagination__link--arrow"
         href="#" :class="{'pagination__link--disabled': page === pages}"
         aria-label="Следующая страница" @click.prevent="nextPaginate(page)">
        <svg width="8" height="14" fill="currentColor">
          <use xlink:href="#icon-arrow-right"></use>
        </svg>
      </a>
    </li>
  </ul>
</template>

<script>
export default {
  model: {
    prop: 'page',
    event: 'paginate',
  },
  name: 'BasePagination',
  props: ['page', 'count', 'perPage'],
  computed: {
    pages() {
      return Math.ceil(this.count / this.perPage);
    },
  },
  methods: {
    paginate(page) {
      this.$emit('paginate', page);
    },
    nextPaginate(page) {
      if (page === this.pages) {
        this.paginate(page);
      } else {
        this.paginate(page + 1);
      }
    },
    prevPaginate(page) {
      if (page === 1) {
        this.paginate(page);
      } else {
        this.paginate(page - 1);
      }
    },
  },
};
</script>

<style scoped>

</style>

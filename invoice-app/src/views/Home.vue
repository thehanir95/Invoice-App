<template>
  <div class="header-section">
    <div class="title-section">
      <h1>Test Tags Pull</h1>
      <h1 class="title-section-main">Invoices</h1>
      <h4 class="title-section-sub">There are 4 total invoices</h4>
    </div>
    <div class="btn-section">
      <div>
        <div class="btn-group">
          <button
            type="button"
            class="btn btn-warning dropdown-toggle"
            data-toggle="dropdown"
            aria-haspopup="true"
            aria-expanded="true"
            @click="filterMenu"
          >
          Filter By Status
          </button>
          <div class="dropdown-menu">
            <a class="dropdown-item" href="#">Draft</a>
            <a class="dropdown-item" href="#">Pending</a>
            <a class="dropdown-item" href="#">Paid</a>
            <a class="dropdown-item" href="#">Clear filter</a>
          </div>
        </div>
      </div>
      <div>
        <button type="button" class="btn btn-info" @click="createNewInvoice">New Invoice</button>
      </div>
    </div>
  </div>
</template>

<script>
import { mapMutations } from 'vuex';
export default {
  name: "Home",
  methods:{
    ...mapMutations(['TOGGLE_INVOICE']),
    createNewInvoice() {
        this.TOGGLE_INVOICE()
    },
    filterMenu() {
        alert('filter')
    }
  },
};
</script>

<style lang="scss" scoped>
.header-section {
  width: 100%;
  display: flex;
  align-items: center;
}
.title-section,
.btn-section {
  width: 50%;
}
.btn-section {
  display: flex;
  justify-content: space-evenly;
}
.title-section {
  text-align: left;
}
.title-section-main {
  margin: 0;
}
.title-section-sub {
  margin: 0;
}
</style>

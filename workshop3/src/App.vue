<template>
  <div id="app">
    <div class="container">
      <h2 align="center">Workshop #3 - Calculate Product's Price</h2>
      <hr />
      <div class="row">
        <div class="col-md-3" v-for:="item in products">
          <div class="card h-100">
            <img :src="item.image" class="card-img-top" />
            <div class="card-body">
              <h4 class="card-title">{{ item.name }}</h4>
              <p class="card-text">price {{ item.price }} baht</p>
            </div>
            <div class="card-footer">
              <div class="form-check form-switch">
                <input
                  class="form-check-input"
                  type="checkbox"
                  @change="selected(item)"
                />
              </div>
            </div>
          </div>
        </div>
        <div class="col">
          <h2>Total price {{ total() }} baht</h2>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      products: [
        {
          id: 1,
          name: "black coffee",
          price: 30,
          image: "https://f.ptcdn.info/561/064/000/ptbtmq1ba4C4z40CC3pe-o.jpg",
          active: false,
        },
        {
          id: 2,
          name: "ice tea",
          price: 35,
          image:
            "https://img-global.cpcdn.com/recipes/11543ee5aaa4b4f5/751x532cq70/%E0%B8%A3%E0%B8%B9%E0%B8%9B-%E0%B8%AB%E0%B8%A5%E0%B8%B1%E0%B8%81-%E0%B8%82%E0%B8%AD%E0%B8%87-%E0%B8%AA%E0%B8%B9%E0%B8%95%E0%B8%A3-%E0%B8%8A%E0%B8%B2%E0%B9%80%E0%B8%A2%E0%B9%87%E0%B8%99-%E0%B8%AB%E0%B8%A3%E0%B8%B7%E0%B8%AD-%E0%B8%8A%E0%B8%B2%E0%B8%99%E0%B8%A1%E0%B9%80%E0%B8%A2%E0%B9%87%E0%B8%99.jpg",
          active: false,
        },
      ],
    };
  },
  methods: {
    selected: function (item) {
      item.active = !item.active;
    },
    total: function () {
      var sum = 0;
      this.products.forEach(function (item) {
        if (item.active) {
          sum += item.price;
        }
      });
      return sum;
    },
  },
};
</script>


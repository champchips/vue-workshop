<template>
  <div id="app">
    <div class="container">
      <h2 align="center">Workshop #4 - Cart Product</h2>
      <hr />
      <div class="row">
        <div class="col-md-2" v-for:="item in products">
          <div class="card h-100">
            <img :src="item.image" class="card-img-top" />
            <div class="card-body">
              <h4 class="card-title">{{ item.name }}</h4>
              <p class="card-text">price {{ item.price }} baht</p>
            </div>
            <div class="card-footer">
              <button class="btn btn-success" @click="addCart(item)">
                Add Cart
              </button>
            </div>
          </div>
        </div>
        <div class="col-md-8" v-if="carts != 0">
          <h3 align="center">Cart</h3>
          <table class="table table-hover">
            <thead>
              <tr class="table-dark">
                <th scope="col">Image</th>
                <th scope="col">Name</th>
                <th scope="col">Price</th>
                <th scope="col" align="center">Amount</th>
                <th scope="col">Total</th>
                <th scope="col">Remove</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="product in carts">
                <td>
                  <img :src="product.image" alt="" width="100" height="80" />
                </td>
                <td>{{ product.name }}</td>
                <td>{{ product.price }}</td>
                <td>
                  <button
                    class="btn btn-dark qty-minus"
                    @click="minusQty(product)"
                  >
                    -
                  </button>
                  {{ product.qty }}
                  <button
                    class="btn btn-dark qty-plus"
                    @click="plusQty(product)"
                  >
                    +
                  </button>
                </td>
                <td>{{ product.total }}</td>
                <td>
                  <button
                    class="btn btn-danger"
                    @click="removeProduct(product)"
                  >
                    Remove
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
          <h3 align="right">Total: {{ total() }} baht</h3>
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
      carts: [],
      coffee: 0,
      tea: 0,
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
    addCart: function(item) {
      if (item.id == 1) {
        this.coffee += 1;
        if (this.coffee <= 1) {
          this.pushData(item);
        } else {
          var found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].price * this.carts[found].qty;
        }
      } else {
        this.tea += 1;
        if (this.tea <= 1) {
          this.pushData(item);
        } else {
          var found = this.findIndex(item);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].price * this.carts[found].qty;
        }
      }
    },
    pushData(product) {
      this.carts.push({
        id: product.id,
        name: product.name,
        price: product.price,
        image: product.image,
        qty: 1,
        total: product.price,
      });
    },
    findIndex: function(item) {
      for (var i = 0; i < this.carts.length; i++) {
        if (this.carts[i].id == item.id) {
          return i;
        }
      }
      return -1;
    },
    minusQty(product) {
      var found = this.findIndex(product);
      if (this.carts[found].qty > 1) {
        this.carts[found].qty -= 1;
        this.carts[found].total =
          this.carts[found].price * this.carts[found].qty;
      }
    },
    plusQty(product) {
      var found = this.findIndex(product);
      this.carts[found].qty += 1;
      this.carts[found].total = this.carts[found].price * this.carts[found].qty;
    },
    removeProduct(product) {
      if (confirm("Are you sure you want to remove this product from Cart ?")) {
        var index = this.carts.indexOf(product);
        this.carts.splice(index, 1);
        if (product.id == 1) {
          this.coffee = 0;
        } else {
          this.tea = 0;
        }
      }
    },
    total: function() {
      var sum = 0;
      this.carts.forEach(function(item) {
        sum += item.total;
      });
      return sum;
    },
  },
};
</script>
<style scoped>
.qty-minus {
  margin-right: 5px;
}
.qty-plus {
  margin-left: 5px;
}
</style>

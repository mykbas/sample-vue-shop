<template>
  <main class="capsule">
    <app-masthead img="banner-ppl-women" title="Women's" bkcolor="#e82319"/>
    <div class="contain">
      <app-sidebar :pricerange.sync="highprice"/>
      <transition-group name="items" tag="section" class="content">
        <app-item 
          v-for="(item, index) in wProducts"
          key="item"
          :item="item"
          :index="index"
        />
      </transition-group>
    </div>
  </main>
</template>

<script>
import AppSidebar from './../components/AppSidebar.vue';
import AppMasthead from './../components/AppMasthead.vue';
import AppItem from './../components/AppItem.vue';

export default {
  components: {
    AppSidebar,
    AppMasthead,
    AppItem
  },
  data() {
    return {
      highprice: 300
    };
  },
  computed: {
    wProducts() {
      let temp = [];
      this.$store.getters.women.forEach(el => {
        if (this.$store.state.sale) {
          if (el.price < this.highprice && el.sale) {
            temp.push(el);
          }
        } else {
          if (el.price < this.highprice) {
            temp.push(el);
          }
        }
      });
      return temp;
    }
  }
};
</script>

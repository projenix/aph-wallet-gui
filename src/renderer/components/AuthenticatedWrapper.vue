<template>
  <section id="authenticated-wrapper">
    <sidebar></sidebar>
    <div class="content">
      <portfolio-header></portfolio-header>
      <router-view></router-view>
    </div>
  </section>
</template>

<script>
import PortfolioHeader from './PortfolioHeader';
import Sidebar from './Sidebar';

export default {
  components: {
    PortfolioHeader,
    Sidebar,
  },

  mounted() {
    this.$services.neo.fetchNEP5Tokens();

    if (!this.$services.wallets.getCurrentWallet()) {
      this.$router.push('/login');
    }
  },
};
</script>

<style lang="scss">
#authenticated-wrapper {
  display: flex;
  flex-direction: row;

  #sidebar {
    flex: none;
    width: toRem(300px);
  }

  .content {
    background: $light-grey;
    display: flex;
    flex-direction: column;
    flex: 1;
  }
}
</style>

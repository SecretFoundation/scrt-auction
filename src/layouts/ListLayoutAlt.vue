<template>
  <default-layout>
    <page>
        <column class="auctions-filter" mode="full">
            <block>
                <auctions-filter></auctions-filter>
            </block>
        </column>

        <column>
            <block>
                <div class="auctions-set" :class="auctionsFilter.viewMode">
                    <slot></slot>
                </div>
            </block>
        </column>
    </page>
  </default-layout>
</template>

<script>

import AuctionItem from '../components/AuctionItem.vue'
import AuctionsFilter from '../components/AuctionsFilter.vue';
import KeplrAccount from '../components/KeplrAccount.vue';

export default {
  components: { AuctionItem, KeplrAccount, AuctionsFilter },
  props: [ "auctionsFilter" ],
  metaInfo: {
    title: 'Secret Auctions',
  },
  data() {
    return {
      keplrAccount: null
    }
  },
  methods: {
    clearFilters() {
      this.auctionsFilter.sellToken = "";
      this.auctionsFilter.bidToken = "";
    },
  }
}
</script>

<style lang="scss" scoped>
  @import "@lkmx/flare/src/functions/respond-to";

  .auction-new {
    border: 2px solid black;
  }

  .auctions-set {
    display: grid;
    grid-gap: var(--f-gutter);
    margin: var(--f-gutter) 0; 

    &.grid {
      @include respond-to("<=s") {
        grid-template-columns: 1fr;
      }
      @include respond-to("m") {
        grid-template-columns: repeat(2, 1fr);
      }
      @include respond-to(">m") {
        grid-template-columns: repeat(3, 1fr);
      }
    }
  }

  .auctions-filter {
    background-color: rgba(0,0,0, 0.7);
    position: sticky;
    top: 0;
    z-index: 1000;
  }


</style>

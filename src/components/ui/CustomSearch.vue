<template>
  <div class="search">
    <input
        v-model="searchInfo"
        ref="searchInput"
        type="text"
        :placeholder="textPlaceholder"
        class="form-control"
        @keyup.enter="startSearching()"
    >
    <svg
        class="search-find search-icon"
        fill="currentColor"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 88 88"
        @click="startSearching()"
    >
      <path
          d="M85 31.1c-.5-8.7-4.4-16.6-10.9-22.3C67.6 3 59.3 0 50.6.6c-8.7.5-16.7 4.4-22.5 11-11.2 12.7-10.7 31.7.6 43.9l-5.3 6.1-2.5-2.2-17.8 20 9 8.1 17.8-20.2-2.1-1.8 5.3-6.1c5.8 4.2 12.6 6.3 19.3 6.3 9 0 18-3.7 24.4-10.9 5.9-6.6 8.8-15 8.2-23.7zM72.4 50.8c-9.7 10.9-26.5 11.9-37.6 2.3-10.9-9.8-11.9-26.6-2.3-37.6 4.7-5.4 11.3-8.5 18.4-8.9h1.6c6.5 0 12.7 2.4 17.6 6.8 5.3 4.7 8.5 11.1 8.9 18.2.5 7-1.9 13.8-6.6 19.2z"></path>
    </svg>
    <CloseIcon
        v-if="isSearching"
        class="search-close search-icon"
        fill="currentColor"
        @click="stopSearching()"
    />
  </div>
</template>

<script>
  import CloseIcon from "@/components/iconComponents/CloseIcon";

  export default {
    name: "CustomSearch",
    components: {
      CloseIcon
    },
    props: {
      textPlaceholder: {
        type: String,
        default: ''
      }
    },
    data() {
      return {
        searchInfo: '',
        isSearching: false
      }
    },
    watch: {
      searchInfo() {
        if (this.searchInfo.length > 0) {
          this.startSearching()
        } else if (this.searchInfo.length === 0) {
          this.stopSearching()
        }
      }
    },
    methods: {
      startSearching() {
        if (this.searchInfo) {
          this.$emit('start-searching', this.searchInfo)
          this.isSearching = true
        } else {
          this.$refs.searchInput.focus()
        }
      },
      stopSearching() {
        this.isSearching = false
        this.$emit('stop-searching')
        this.searchInfo = ''
      }
    }
  }
</script>

<style lang="scss" scoped>
  .search {
    position: relative;
    border: 1px solid white;
    border-radius: 4px;

    &-icon {
      position: absolute;
      top: 12px;
      right: 12px;
      color: inherit;
    }

    &-close {
      top: 14px;
      right: 40px;
    }

    &-find {
      width: 16px;
      height: 16px;
    }

    @media (max-width: 1024px) {
      width: 100%;
    }
  }

  .white {
    color: #FFF
  }
</style>
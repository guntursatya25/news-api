<template>
  <b-skeleton-wrapper :loading="loading">
    <template #loading>
      <b-row>
        <b-col>
          <b-skeleton width="100%"></b-skeleton>
          <b-skeleton width="100%"></b-skeleton>
          <b-skeleton width="100%" height="12rem"></b-skeleton>
        </b-col>
        <b-col>
          <b-row>
            <b-col>
              <b-skeleton width="70%"></b-skeleton>
              <b-skeleton width="55%"></b-skeleton>
              <b-skeleton width="70%" height="6rem"></b-skeleton>
            </b-col>
            <b-col>
              <b-skeleton width="70%"></b-skeleton>
              <b-skeleton width="55%"></b-skeleton>
              <b-skeleton width="70%" height="6rem"></b-skeleton>
            </b-col>
          </b-row>
          <b-row>
            <b-col>
              <b-skeleton width="70%"></b-skeleton>
              <b-skeleton width="55%"></b-skeleton>
              <b-skeleton width="70%" height="6rem"></b-skeleton>
            </b-col>
            <b-col>
              <b-skeleton width="70%"></b-skeleton>
              <b-skeleton width="55%"></b-skeleton>
              <b-skeleton width="70%" height="6rem"></b-skeleton> </b-col
          ></b-row>
        </b-col>
      </b-row>
     <b-row class="mt-5">
        <b-col>
          <b-row>
            <b-col>
              <b-skeleton width="70%"></b-skeleton>
              <b-skeleton width="55%"></b-skeleton>
              <b-skeleton width="70%" height="6rem"></b-skeleton>
            </b-col>
            <b-col>
              <b-skeleton width="70%"></b-skeleton>
              <b-skeleton width="55%"></b-skeleton>
              <b-skeleton width="70%" height="6rem"></b-skeleton>
            </b-col>
          </b-row>
          <b-row>
            <b-col>
              <b-skeleton width="70%"></b-skeleton>
              <b-skeleton width="55%"></b-skeleton>
              <b-skeleton width="70%" height="6rem"></b-skeleton>
            </b-col>
            <b-col>
              <b-skeleton width="70%"></b-skeleton>
              <b-skeleton width="55%"></b-skeleton>
              <b-skeleton width="70%" height="6rem"></b-skeleton> </b-col
          ></b-row>
        </b-col>
        <b-col>
          <b-skeleton width="100%"></b-skeleton>
          <b-skeleton width="100%"></b-skeleton>
          <b-skeleton width="100%" height="12rem"></b-skeleton>
        </b-col>
     </b-row>
    </template>
  </b-skeleton-wrapper>
</template>

<script>
export default {
  name: "LoadingComponent",
  data() {
    return {
      loading: false,
      loadingTime: 0,
      maxLoadingTime: 3,
    };
  },
  watch: {
    loading(newValue, oldValue) {
      if (newValue !== oldValue) {
        this.clearLoadingTimeInterval();

        if (newValue) {
          this.$_loadingTimeInterval = setInterval(() => {
            this.loadingTime++;
          }, 1000);
        }
      }
    },
    loadingTime(newValue, oldValue) {
      if (newValue !== oldValue) {
        if (newValue === this.maxLoadingTime) {
          this.loading = false;
        }
      }
    },
  },
  created() {
    this.$_loadingTimeInterval = null;
  },
  mounted() {
    this.startLoading();
  },
  methods: {
    clearLoadingTimeInterval() {
      clearInterval(this.$_loadingTimeInterval);
      this.$_loadingTimeInterval = null;
    },
    startLoading() {
      this.loading = true;
      this.loadingTime = 10;
    },
  },
};
</script>

<style></style>

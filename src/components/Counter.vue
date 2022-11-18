<template lang="">
    <div>
      <h3 v-if="loaded">
          <div v-if="!expired">Buy now</div>
          <div v-else>Timer is done</div>
            {{displayDays}}:
            {{displayHours}}:
            {{displayMinutes}}:
            {{displaySeconds}}
        </h3>
    </div>
</template>
<script>
export default {
  name: "Counter",
  props: ["year", "month", "date", "hours", "minute", "second", "milisecond"],

  data: () => ({
    displayDays: 0,
    displayHours: 0,
    displayMinutes: 0,
    displaySeconds: 0,
    loaded: false,
    expired: false
  }),
  computed: {
    _seconds: () => 1000,
    _minutes() {
      return this._seconds * 60;
    },
    _hours() {
      return this._minutes * 60;
    },
    _days() {
      return this._hours * 24;
    },
    end() {
      return new Date(
        this.year,
        this.month,
        this.date,
        this.hours,
        this.minute,
        this.second,
        this.milisecond
      );
    },
  },
  methods: {
    formatNum(num) {
      return num < 10 ? "0" + num : num;
    },

    showRemining() {
      const timer = setInterval(() => {
        const now = new Date();
        // const end = new Date(2022, 10, 19, 9, 16, 0)
        const distance = this.end.getTime() - now.getTime();

        if (distance < 0) {
          clearInterval(timer);
          this.expired = true
          this.loaded = true
          return;
        }

        const seconds = Math.floor((distance % this._minutes) / this._seconds);
        const minutes = Math.floor((distance % this._hours) / this._minutes);
        const hours = Math.floor((distance % this._days) / this._hours);
        const days = Math.floor(distance / this._days);

        this.displaySeconds = this.formatNum(seconds);
        this.displayMinutes = this.formatNum(minutes);
        this.displayHours = this.formatNum(hours);
        this.displayDays = this.formatNum(days);
        this.loaded = true;
      }, 1000);
    },
  },
  mounted() {
    this.showRemining();
  },
};
</script>
<style lang="">
</style>
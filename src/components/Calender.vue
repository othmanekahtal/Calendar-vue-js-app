<template>
  <Title text='Calender'/>
  <div class="calender-box calender-box-view">
    <div class="year">{{ getCurrentYearDynamic }}</div>
    <div class="month">{{ getCurrentMonthName }}</div>
  </div>
  <section class="calender">
    <div class="calender__days">
      <span v-for="day in  days" :key="day" class="calender__day">{{ day }}</span>
      <span class="calender__day-number calender__day-number--out" v-for="day in getPreviousDays"
            :key="day">{{ day }}</span>
      <span  v-for="number in getNumberOfDays" :class="number===getCurrentDay && currentDate === getChangedDate?'calender__day-number calender__day-number--active':'calender__day-number'"
            :key="number">{{ ('' + number).padStart(2, '0') }}</span>
      <span class="calender__day-number calender__day-number--out" v-for="number in getNextDays"
            :key="number">{{ ('' + number).padStart(2, '0') }}</span>
    </div>
  </section>
  <div class="calender-box calender-box-control">
    <button class="btn btn--previous" @click="previous">Pre.</button>
    <button class="btn btn--next" @click="next">Nex.</button>
  </div>
</template>
<script>
import Title from './Title';

export default {
  components: {
    Title
  },
  data() {
    return {
      currentDate: new Intl.DateTimeFormat(navigator.language, {
        year: 'numeric',
        month: 'numeric',
        day: 'numeric'
      }).format(),
      getCurrentYear: new Date().getFullYear(),
      getCurrentMonth: new Date().getMonth(),
      getCurrentDay: new Date().getDate(),
      days: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
    }
  },
  methods: {
    next() {
      // console.log(this.currentDate);
      this.getCurrentMonth++
    },
    previous() {
      this.getCurrentMonth--
    },
  },
  computed: {
    getNumberOfDays() {
      return new Date(this.getCurrentYear, this.getCurrentMonth + 1, 0).getDate();
    },
    getStartedDay() {
      return new Date(this.getCurrentYear, this.getCurrentMonth, 1).getDay();
    },
    getPreviousDays() {
      let daysRange = [];
      let lastDate = new Date(this.getCurrentYear, this.getCurrentMonth, 0).getDate();
      let StartDate = lastDate - this.getStartedDay + 1;
      for (let i = StartDate; i <= lastDate; i++) {
        daysRange.push(i)
      }
      return daysRange;
    },
    getNextDays() {
      let daysRange = [];
      let lastDate = new Date(this.getCurrentYear, this.getCurrentMonth + 1, 0).getDay();
      for (let i = 1; i <= 6 - lastDate; i++) {
        daysRange.push(i)
      }
      // console.log(daysRange,lastDate)
      return daysRange;
    },
    getCurrentMonthName() {
      return new Intl.DateTimeFormat(navigator.language, {month: 'long'}).format(new Date(this.getCurrentYear, this.getCurrentMonth))
    },
    getCurrentYearDynamic() {
      return new Intl.DateTimeFormat(navigator.language, {year: 'numeric'}).format(new Date(this.getCurrentYear, this.getCurrentMonth))
    },
    getChangedDate() {
      return new Intl.DateTimeFormat(navigator.language, {
        year: 'numeric',
        month: 'numeric',
        day: 'numeric'
      }).format(new Date(+this.getCurrentYearDynamic, this.getCurrentMonth, this.getCurrentDay))
    }
  }
}
</script>
<style lang="scss" scoped>
.calender-box {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 1.9rem;
  font-weight: 700;
  padding: 1rem 2.5rem;
  margin-bottom: 1rem;

  &-view {
    color: #f5f5f5;
    background-color: #444444;
    border-radius: 5px;
  }

  &-control {
    .btn {
      all: unset;
      cursor: pointer;
      border-radius: 5px;
      padding: 5px 10px;
      background-color: #f5f5f5;
      box-shadow: 0 0 1.5rem rgba(68, 66, 66, 0.33);
    }
  }
}

.calender {
  padding: 1.5rem 0;

  &__days {
    display: grid;
    grid-column-gap: 1.5rem;
    grid-row-gap: 2.5rem;
    grid-template-columns: repeat(7, 1fr);
  }

  .calender__day-number {
    padding: 1rem;

    &--out {
      color: rgba(#444, .25);
    }

    &--active {
      background-color: rgba(#444444, .65);
      font-weight: 800;
      color: #f5f5f5;
      border-radius: 5rem;
      box-shadow: 0 0 5px rgba(#444, .35);
    }
  }
}
</style>
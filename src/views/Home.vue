<template>
  <div class="w-50 m-auto">
    <div class="form-group">
      <h6>Aankomsttijd</h6>
      <input
        type="time"
        class="form-control text-center"
        v-model="aankomsttijd"
        @change="clearVertrektijd"
      />
    </div>
    <div class="form-group mt-5">
      <h6>Duurtijd</h6>
      <input
        type="time"
        class="form-control text-center"
        v-model="duurtijd"
        @change="clearVertrektijd"
      />
    </div>
    <n-button class="mt-5" @click="berekenTijd">Bereken vertrektijd</n-button>
  </div>

  <div v-if="vertrektijd !== null" class="mt-5">
    <h2>Vertrektijd is {{ this.vertrektijd }}</h2>
  </div>
</template>

<script>
// @ is an alias to /src
import { NButton } from "naive-ui";
export default {
  name: "Home",
  components: {
    NButton,
  },
  data() {
    return {
      aankomsttijd: null,
      duurtijd: null,
      vertrektijd: null,
    };
  },
  methods: {
    berekenTijd() {
      var num = Math.abs(
        this.differenceInMinutes(this.aankomsttijd, this.duurtijd)
      );
      var hours = num / 60;
      var rhours = Math.floor(hours);
      var minutes = (hours - rhours) * 60;
      var rminutes = Math.round(minutes);
      if (rminutes <= 9) {
        rminutes = `0${rminutes}`;
      } else {
        rminutes = rminutes;
      }

      this.vertrektijd = `${rhours}:${rminutes}`;
    },
    differenceInMinutes(start, end) {
      var totalMinutes = function (value) {
        var match = /(\d{1,2}):(\d{1,2})/g.exec(value);
        return Number(match[1]) * 60 + Number(match[2]);
      };
      return totalMinutes(end) - totalMinutes(start);
    },
    clearVertrektijd() {
      this.vertrektijd = null;
    },
  },
  computed: {},
};
</script>

<template>
  <div>
    <b-container class="mt-3">
      <b-row>
        <b-col>
          <b-card>
            <b-card-text>
              <b-row>
                <b-col cols="12" md="6" sm="6" class="offset-md-2">
                  <cleave
                    v-model="step"
                    :options="options"
                    class="form-control mr-1"
                    placeholder="Step"
                  ></cleave>
                  <small class="error" v-if="!$v.step.maxLength">
                    Step must have equal or lower than 6 digits.
                  </small>
                </b-col>
                <b-col cols="12" md="3" sm="3">
                  <b-button
                    variant="outline-primary"
                    @click="addStep"
                    :disabled="!$v.step.maxLength"
                  >
                    Add Counter
                  </b-button>
                </b-col>
                <b-col cols="10" class="offset-md-2">
                  <small>
                    (This only accept numbers like: 1, 2, -5, 3.8, 310)
                  </small>
                </b-col>
              </b-row>
              <b-row class="mt-5">
                <b-col
                  cols="12"
                  sm="6"
                  md="3"
                  v-for="(step, i) in steps"
                  :key="i"
                >
                  <b-card :header="`step: ${step.step}`">
                    <div class="text-center step-value">
                      {{ step.value }}
                    </div>
                    <b-button variant="primary" block @click="run(step)"
                      >Run</b-button
                    >
                  </b-card>
                </b-col>
              </b-row>
            </b-card-text>
          </b-card>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>
<script>
import { maxLength } from "vuelidate/lib/validators";
import Cleave from "vue-cleave-component";
export default {
  name: "Step",
  components: {
    Cleave,
  },
  data: () => ({
    step: "",
    steps: [],
    options: {
      numeral: true,
      numeralDecimalScale: 1,
      numeralThousandsGroupStyle: "thousand",
    },
  }),
  validations: {
    step: {
      maxLength: maxLength(6),
    },
  },
  methods: {
    addStep: function() {
      this.steps.push({
        step: parseFloat(this.step),
        value: 0,
      });
    },
    run: function(step) {
      step.value += step.step;
    },
  },
};
</script>
<style scoped>
.step-value {
  font-size: 80px;
  padding-top: 20px;
  padding-bottom: 60px;
}
.error {
  color: #bb1111;
}
</style>

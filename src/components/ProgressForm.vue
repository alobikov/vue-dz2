<template>
  <div>
    <div class="q-pa-md container q-gutter-sm column">
      <div class="progress"></div>

      <div
        v-for="(info, key) in infos"
        class="col"
        :key="info[key]"
        @input="validate(key)"
      >
        <div class="q-pb-xs">
          <label class="text-subtitle2">{{ info.name }}</label>
          <q-icon
            v-show="!!info.value"
            :class="info.class"
            name="check_circle"
          />
        </div>
        <input type="text" v-model="info['value']" />
      </div>

      <div class="col q-mt-md">
        <q-btn color="teal">Send Data</q-btn>
      </div>
    </div>
    <div class="q-pa-md container q-gutter-sm column">
      <q-list bordered separator>
        <q-item v-for="(info, key) in infos" :key="info[key]">{{
          info.value
        }}</q-item>
      </q-list>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProgressForm",
  methods: {
    validate(key) {
      if (this.infos[key].value.length > 0) {
        if (this.infos[key].pattern.test(this.infos[key].value))
          this.infos[key].class = "green";
        else this.infos[key].class = "red";
      }
    }
  },
  data: function() {
    return {
      infos: [
        {
          name: "Name",
          value: "",
          pattern: /^[a-zA-Z]{2,30}$/,
          class: ""
        },
        {
          name: "Phone",
          value: "",
          pattern: /^[0-9]{7,14}$/,
          class: ""
        },
        {
          name: "Email",
          value: "",
          pattern: /.+/,
          class: ""
        },
        { name: "Some Field 1", value: "", patter: /.+/, class: "" },
        { name: "Some Field 2", value: "", patter: /.+/, class: "" }
      ]
    };
  }
};
</script>

<style>
.box {
  border: 1px solid #222;
}
.col-auto + .col-auto {
  margin-top: 10px;
}
.col-auto {
  width: 300px;
}
input {
  width: 100%;
  border: 1px solid #ccc;
}
.green {
  color: green;
}
.red {
  color: red;
}
.container {
  margin-left: 10rem;
  margin-top: 2rem;
  width: 50%;
}
.progress {
  border: 1px solid #ccc;
  background-color: #ccc;
  height: 28px;
}
</style>

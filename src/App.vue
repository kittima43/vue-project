<template>
  <div class="app-container">
    <div class="text-frame">
    <p>{{ message }}</p>
    </div>
    <div>
      <center>
        <h1>test program</h1>
        <br>
        <span class="input-group-text" id="inputGroup-sizing-sm">ใส่เลข:</span>
        <input type="number" v-model="rows">
        <button @click="submit" class="btn-Submit">Submit</button>
        <ul v-if="showPyramids">
          <div class="pyramid-container">
            <h2></h2>
            <ul v-for="(row, App) in pyramid" :key="App">
              <span v-for="num in row" :key="num" class="diamond">💎</span>
            </ul>
          </div>
          <div class="pyramid-container">
            <ul v-for="(row, App) in reversedPyramid" :key="App">
              <span v-for="(num, numIndex) in row" :key="numApp" class="diamond">
                {{ num }}
              </span>
            </ul>
          </div>
        </ul>
      </center>
      <div v-if="pyramid.length === 0 && reversedPyramid.length === 0"></div>
    </div>
  </div>
</template>

<style>
.pyramid-container {
  max-width: 960px;
  margin-bottom: -1px;
  background: black;
  border: 1 px solid black;
  padding: 3 rem
}

.template {
  background: black;
}

.btn-Submit {
  max-width: 960px;
  background: green;
  padding: 3 rem
}

h2 {
  margin-bottom: 10px;
}

</style>
<script>
export default {
  data() {
    return {
      rows: 0,
      pyramid: [],
      reversedPyramid: [],
      showPyramids: false,
    };
  },
  methods: {
    generatePyramids() {
      const rows = parseInt(this.rows);
      if (!isNaN(rows) && rows > 0) {
        let pyramid = [];
        let reversedPyramid = [];
        let prev = "";
        let curr = "💎";

        for (let i = 0; i < rows; i++) {
          let row = [];
          let reversedRow = [];
          for (let j = 0; j <= i; j++) {
            row.push(curr);
            reversedRow.unshift(curr);
            let temp = curr;
            curr = temp;
            prev = temp;
          }
          pyramid.push(row);
          reversedPyramid.push(reversedRow);
        }

        this.pyramid = pyramid;
        this.reversedPyramid = reversedPyramid.reverse();
      } else {
        this.pyramid = [];
        this.reversedPyramid = [];
      }
    },
    submit() {
      this.generatePyramids();
      this.showPyramids = true;
    },
  },
};
</script>
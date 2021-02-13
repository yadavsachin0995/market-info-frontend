<template>
  <div>
    <input
      type="text"
      id="search-bar"
      placeholder="Search By Name ..."
      v-on:keyup="executeSearch()"
    />

    <button @click="handleDownload('export.csv')">Download</button>

    <table style="width: 100%" id="t01" v-if="equityDetails != 'None'">
      <tr>
        <th>SC_CODE</th>
        <th>SC_NAME</th>
        <th>OPEN</th>
        <th>HIGH</th>
        <th>LOW</th>
        <th>CLOSE</th>
      </tr>
      <tr v-for="equityDetail in equityDetails" :key="equityDetail.SC_CODE">
        <td>{{ equityDetail.SC_CODE }}</td>
        <td>{{ equityDetail.SC_NAME }}</td>
        <td>{{ equityDetail.OPEN }}</td>
        <td>{{ equityDetail.HIGH }}</td>
        <td>{{ equityDetail.LOW }}</td>
        <td>{{ equityDetail.CLOSE }}</td>
      </tr>
    </table>
  </div>
</template>

<script>

export default {
  name: "EquityDetails",
  props: ["equityDetails"],
  methods: {
    executeSearch: function () {
      var input, filter, table, tr, td, i, txtValue;
      input = document.getElementById("search-bar");
      filter = input.value.toUpperCase();
      table = document.getElementById("t01");
      tr = table.getElementsByTagName("tr");

      for (i = 0; i < tr.length; i++) {
        td = tr[i].getElementsByTagName("td")[1];
        if (td) {
          txtValue = td.textContent || td.innerText;
          if (txtValue.toUpperCase().indexOf(filter) > -1) {
            tr[i].style.display = "";
          } else {
            tr[i].style.display = "none";
          }
        }
      }
    },

    handleDownload: function (filename) {
      var csv = [];
      var table = document.getElementById("t01");
      var rows = table.getElementsByTagName("tr");
      rows = Object.values(rows).filter((o) => o.style.display != "none");

      for (var i = 0; i < rows.length; i++) {
        var row = [],
          cols = rows[i].querySelectorAll("td, th");

        for (var j = 0; j < cols.length; j++) row.push(cols[j].innerText);

        csv.push(row.join(","));
      }
      this.downloadCSV(csv.join("\n"), filename);
    },

    downloadCSV: function (csv, filename) {
      var csvFile;
      var downloadLink;

      csvFile = new Blob([csv], { type: "text/csv" });
      downloadLink = document.createElement("a");
      downloadLink.download = filename;
      downloadLink.href = window.URL.createObjectURL(csvFile);
      downloadLink.style.display = "none";
      document.body.appendChild(downloadLink);
      downloadLink.click();
    },
  },
};
</script>

<style scoped>
table,
th,
td {
  font-size: smaller;
  border: 0.5px solid black;
  border-collapse: collapse;
}

th,
td {
  padding: 5px;
}

table {
  border-spacing: 5px;
}

#t01 {
  width: 100%;
  margin-top: 15%;
}

#t01 tr:nth-child(even) {
  background-color: #eee;
}
#t01 tr:nth-child(odd) {
  background-color: #fff;
}
#t01 th {
  color: white;
  background-color: black;
  text-align: left;
}

input[type="text"] {
  float: left;
  padding: 6px;
  margin-top: 8px;
  margin-bottom: 8px;
  font-size: 15px;
  width: 30%;
  border: 0.5px solid black;
}

button {
  float: right;
  padding: 6px;
  margin-top: 8px;
  margin-bottom: 8px;
  font-size: 15px;
  width: 15%;
  background-color: #42b983;
  color: white;
  border: none;
  font-weight: bolder;
}
</style>
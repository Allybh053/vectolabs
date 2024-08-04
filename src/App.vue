<template>
  <div id="app">
    <h1>Asset List</h1>
    <table>
      <thead>
        <tr>
          <th>Asset Name</th>
          <th>Department</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(asset, index) in assets" :key="index">
          <td>{{ asset.name }}</td>
          <td>{{ asset.department }}</td>
        </tr>
      </tbody>
    </table>
    <button @click="downloadCSV">Download CSV</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      assets: [
        { name: 'Printer', department: 'HR' },
        { name: 'Monitor', department: 'IT' },
        { name: 'Barcode Scanner', department: 'ACCOUNT' },
      ],
    };
  },
  methods: {
    downloadCSV() {
      const csvContent = 'data:text/csv;charset=utf-8,' +
        ['Asset name,Department']
          .concat(this.assets.map(a => `${a.name},${a.department}`))
          .join('\n');
      const encodedUri = encodeURI(csvContent);
      const link = document.createElement('a');
      link.setAttribute('href', encodedUri);
      link.setAttribute('download', 'assets.csv');
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
table {
  margin: 0 auto;
  border-collapse: collapse;
}
th, td {
  border: 1px solid #ddd;
  padding: 8px;
}
th {
  background-color: #f2f2f2;
}
</style>

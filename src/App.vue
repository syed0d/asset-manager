<template>
  <div class="asset-list">
    <h2>Asset List</h2>
    <table>
      <thead>
        <tr>
          <th>Asset name</th>
          <th>Department</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="asset in assets" :key="asset.id">
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
  name: 'App',
  data() {
    return {
      assets: [
        { id: 1, name: 'Printer', department: 'HR' },
        { id: 2, name: 'Monitor', department: 'IT' },
        { id: 3, name: 'Barcode Scanner', department: 'ACCOUNT' }
      ]
    };
  },
  methods: {
    downloadCSV() {
      const header = ['Asset name', 'Department'];
      const csv = [
        header.join(','),
        ...this.assets.map(asset => [asset.name, asset.department].join(','))
      ].join('\n');
      
      const blob = new Blob([csv], { type: 'text/csv' });
      const url = window.URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.style.display = 'none';
      a.href = url;
      a.download = 'assets.csv';
      document.body.appendChild(a);
      a.click();
      window.URL.revokeObjectURL(url);
      document.body.removeChild(a);
    }
  }
};
</script>

<style>
.asset-list {
  margin: 20px;
}
table {
  width: 100%;
  border-collapse: collapse;
}
th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}
th {
  background-color: #f2f2f2;
}
button {
  margin-top: 10px;
  padding: 8px 16px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
}
button:hover {
  background-color: #45a049;
}
</style>

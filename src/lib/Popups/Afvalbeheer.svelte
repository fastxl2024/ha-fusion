<script lang="ts">
  let tableData = [
    { name: 'Alice', age: 25, city: 'Amsterdam' },
    { name: 'Bob', age: 30, city: 'Rotterdam' },
    { name: 'Charlie', age: 22, city: 'Utrecht' },
    { name: 'David', age: 28, city: 'The Hague' }
  ];
</script>

<table>
  <thead>
    <tr>
      <th>Naam</th>
      <th>Leeftijd</th>
      <th>Stad</th>
    </tr>
  </thead>
  <tbody>
    {#each tableData as person}
      <tr>
        <td>{person.name}</td>
        <td>{person.age}</td>
        <td>{person.city}</td>
      </tr>
    {/each}
  </tbody>
</table>

<style>
  table {
    border-collapse: collapse;
    width: 100%;
  }
  th, td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
  }
  th {
    background-color: #f2f2f2;
  }
</style>
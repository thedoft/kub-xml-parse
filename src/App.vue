<template>
  <el-main>
    <span v-if="error">{{ error }}</span>
    <el-table v-else :data="data" border fit style="width: 100%">
      <el-table-column prop="ID" label="Артикул" />
      <el-table-column prop="NAME" label="Наименование" min-width="300px" />
      <el-table-column prop="QUANTITY" label="Общий остаток" />
      <el-table-column prop="FREE_QUANTITY" label="Свободный остаток" />
      <el-table-column prop="RESERVED_QUANTITY" label="В резерве" />
      <el-table-column prop="INCOME_QUANTITY" label="Ожидаемый приход" />
      <el-table-column prop="DATE_INCOME" label="Ожидаемая дата прихода" />
      <el-table-column prop="PRICE_FOR_PARTNER" label="Цена для партнеров" />
      <el-table-column prop="PRICE_MRC" label="Цена розничная" />
    </el-table>
  </el-main>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  components: {},
  data() {
    return {
      data: null,
      error: null,
    };
  },
  async mounted() {
    try {
      const { data } = await axios.get('https://kub-xml-parse.herokuapp.com/');
      console.log(data);
    } catch {
      this.error = 'Не удалось загрузить информацию';
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px 0;
}

.el-table .cell {
  word-break: normal !important;
}
</style>

<script>
  import mdParser from "../util/md-parser";
  import { onMount } from "svelte";
  import SQLite from "tauri-plugin-sqlite-api";

  import { Link } from "svelte-routing";

  export let id;

  let rows = [];

  let query = `SELECT * FROM lekce WHERE id = ?`;

  let parsed;

  onMount(async () => {
    const db = await SQLite.open("./hanzi.db");

    rows = await db.select(query, [id]);

    console.log(rows[0].markdown);
    parsed = mdParser(rows[0].markdown);
  });
</script>

<div class="bg-gradient-to-r from-purple-100 to-white flex">
  <div class="pr-5 pl-10 pt-20 basis-2/12">
    <ul class="pl-0">
      <li><Link to="/lekce/1">Lekce 1</Link></li>
      <li><Link to="/lekce/2">Lekce 2</Link></li>
      <li><Link to="/lekce/3">Lekce 3</Link></li>
      <li><Link to="/lekce/4">Lekce 4</Link></li>
      <li><Link to="/lekce/5">Lekce 5</Link></li>
      <li><Link to="/lekce/6">Lekce 6</Link></li>
      <li><Link to="/lekce/7">Lekce 7</Link></li>
    </ul>
  </div>

  <div class="border-2 border-solid p-5 bg-white mt-20 border-black basis-8/12">
    <h1>{id}</h1>
    <div>{@html parsed}</div>
  </div>

  <div class="pr-5 pl-10 pt-20 basis-2/12" />
</div>

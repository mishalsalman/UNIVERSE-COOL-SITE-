<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Universe Search</title>

<style>
  body {
    margin: 0;
    background: #070707;
    color: #fff;
    font-family: Arial, sans-serif;
    text-align: center;
  }

  h1 {
    margin-top: 60px;
    font-size: 45px;
    background: linear-gradient(90deg,#00f2ff,#7a00ff,#00ffea);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    animation: glow 4s infinite alternate;
  }

  @keyframes glow {
    0% { text-shadow: 0 0 10px #00eaff; }
    100% { text-shadow: 0 0 20px #7a00ff; }
  }

  .box {
    margin-top: 30px;
  }

  input {
    width: 70%;
    padding: 14px;
    border-radius: 10px;
    border: 2px solid #00eaff;
    background: #0e0e0e;
    color: white;
    font-size: 18px;
    outline: none;
    box-shadow: 0 0 10px #00eaff;
  }

  button {
    padding: 14px 20px;
    margin-left: 10px;
    border-radius: 10px;
    border: none;
    background: linear-gradient(90deg,#00eaff,#7a00ff);
    color: white;
    font-size: 18px;
    cursor: pointer;
    box-shadow: 0 0 10px #7a00ff;
  }

  #result {
    margin-top: 40px;
    padding: 20px;
    max-width: 600px;
    margin-left: auto;
    margin-right: auto;
    background: #0e0e0e;
    border-radius: 15px;
    box-shadow: 0 0 15px #7a00ff;
  }

  img {
    max-width: 280px;
    margin-top: 15px;
    border-radius: 12px;
    box-shadow: 0 0 15px #00eaff;
  }
</style>
</head>

<body>
<h1>Universe Search 🌌</h1>
<p>Type anything in the universe and discover it instantly!</p>

<div class="box">
  <input id="search" type="text" placeholder="Example: pen, car, tiger, moon...">
  <button onclick="searchItem()">Search</button>
</div>

<div id="result"></div>

<script>
async function searchItem() {
  const query = document.getElementById("search").value;
  const resultBox = document.getElementById("result");

  if (!query.trim()) {
    resultBox.innerHTML = "<p>Please type something.</p>";
    return;
  }

  resultBox.innerHTML = "<p>Loading...</p>";

  try {
    const wiki = await fetch(
      `https://en.wikipedia.org/api/rest_v1/page/summary/${query}`
    ).then(r => r.json());

    const img = wiki.thumbnail ? wiki.thumbnail.source : "";

    resultBox.innerHTML = `
      <h2>${wiki.title || "Not found"}</h2>
      <p>${wiki.extract || "No explanation available."}</p>
      ${img ? `<img src="${img}">` : ""}
    `;
  } catch (e) {
    resultBox.innerHTML = "<p>Error. Try another word.</p>";
  }
}
</script>

</body>
</html>

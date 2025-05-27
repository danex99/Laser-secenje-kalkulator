# Laser-secenje-kalkulator
<!DOCTYPE html>
<html lang="sr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kalkulator laserskog sečenja</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; }
    label { display: block; margin-top: 10px; }
    input { width: 200px; padding: 5px; }
    button { margin-top: 20px; padding: 10px; }
    .rezultat { margin-top: 20px; font-weight: bold; }
  </style>
</head>
<body>
  <h1>Kalkulator laserskog sečenja</h1>

  <label>Cena materijala po kg (€): <input type="number" id="cenaMaterijala"></label>
  <label>Težina materijala (kg): <input type="number" id="tezina"></label>
  <label>Vreme sečenja (min): <input type="number" id="vremeSecenja"></label>
  <label>Cena po min sečenja (€): <input type="number" id="cenaPoMin"></label>
  <label>Broj rupa: <input type="number" id="rupe"></label>
  <label>Cena po rupi (€): <input type="number" id="cenaPoRupi"></label>
  <label>Radna snaga (sati): <input type="number" id="radniSati"></label>
  <label>Cena po satu (€): <input type="number" id="cenaPoSatu"></label>
  <label>Pakovanje (€): <input type="number" id="pakovanje"></label>
  <label>Transport (€): <input type="number" id="transport"></label>
  <label>Rabat (%): <input type="number" id="rabat"></label>
  <label>Marža (%): <input type="number" id="marza"></label>
  <label>PDV (%): <input type="number" id="pdv"></label>

  <button onclick="izracunaj()">Izračunaj</button>

  <div class="rezultat" id="rezultat"></div>

  <script>
    function izracunaj() {
      const materijal = parseFloat(document.getElementById("cenaMaterijala").value) * parseFloat(document.getElementById("tezina").value);
      const secenje = parseFloat(document.getElementById("vremeSecenja").value) * parseFloat(document.getElementById("cenaPoMin").value);
      const rupe = parseFloat(document.getElementById("rupe").value) * parseFloat(document.getElementById("cenaPoRupi").value);
      const rad = parseFloat(document.getElementById("radniSati").value) * parseFloat(document.getElementById("cenaPoSatu").value);
      const pak = parseFloat(document.getElementById("pakovanje").value);
      const trans = parseFloat(document.getElementById("transport").value);

      let trosak = materijal + secenje + rupe + rad + pak + trans;
      const marza = trosak * (parseFloat(document.getElementById("marza").value) / 100);
      let cenaBezPDVa = trosak + marza;
      const rabat = cenaBezPDVa * (parseFloat(document.getElementById("rabat").value) / 100);
      cenaBezPDVa -= rabat;
      const pdv = cenaBezPDVa * (parseFloat(document.getElementById("pdv").value) / 100);
      const konacnaCena = cenaBezPDVa + pdv;

      document.getElementById("rezultat").innerHTML = `
        Ukupni trošak: ${trosak.toFixed(2)} €<br>
        Cena bez PDV-a (nakon marže i rabata): ${cenaBezPDVa.toFixed(2)} €<br>
        PDV: ${pdv.toFixed(2)} €<br>
        <span style="color:green">Konačna cena sa PDV-om: ${konacnaCena.toFixed(2)} €</span>
      `;
    }
  </script>
</body>
</html>

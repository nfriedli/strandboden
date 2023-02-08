+++
title = "test json"
+++

## Prochains départs (dynamique)

<div id="horaire"></div>


<script>
fetch('https://vb-tpb.ch/api/departure/93350/')
  .then(response => response.json())
  .then(data => {
    const departures = data.departures.slice(0, 10);
    let tableHTML = '<table><tr><th>Heure de départ</th><th>Direction</th><th>Ligne</th></tr>';
    departures.forEach(departure => {
      let dateString = departure.time
      let date = new Date(dateString);
      let time = date.toLocaleTimeString();
      tableHTML += `<tr><td>${time}</td><td>${departure.destination.stop_fr_short}</td><td>${departure.line}</td></tr>`;
    });
    tableHTML += '</table>';
    document.querySelector('#horaire').innerHTML = tableHTML;
  })
  .catch(error => console.error(error));
</script>
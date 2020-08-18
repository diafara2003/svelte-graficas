<script>
import Chart from 'chart.js'
import { afterUpdate } from 'svelte'

let datos = []
let chart
let pais = 'usa'
$: url = 'https://covid19.mathdro.id/api/countries/' + pais

async function cargar(){
    await fetch(url)
    .then(r => r.json())
    .then(data => {
        datos = data
        console.log(datos)
    })
    if(chart) chart.destroy()
    let miGrafica = document.getElementById('miGrafica')
    chart = new Chart(miGrafica,{
        type:'bar',
        data:{
            labels:['Fallecidos','Infectados','Recuperados'],
            datasets:[
                {
                    label:'Totales',
                    data:[datos.deaths.value, datos.confirmed.value, datos.recovered.value],
                    backgroundColor:[
                        'red',
                        'yellow',
                        'green'
                    ],borderColor:[
                        'blue',
                        'black',
                        'yellow'
                    ],
                    borderWidth: 2
                }
            ]
        }
    })
}

afterUpdate(cargar)

</script>
<canvas id="miGrafica" width="1" height="1" ></canvas>
<input type="text" bind:value={pais} >
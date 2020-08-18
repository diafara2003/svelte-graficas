<script>
import Chart from 'chart.js'
import { onMount, afterUpdate } from 'svelte'

let index = 0
let nombre = ''
let votos = 0
let datos = [12,23,50,21]
let chart
let max = Math.max(...datos)
function crearGrafica(){
    const miGrafica = document.getElementById('miGrafica')
    chart = new Chart(miGrafica,{
        type:'bar',
        data:{
            labels:['Resident evil','Uncharted','Red Dead Redemption','God of War'],
            datasets: [
                {
                    label:'Número de jugadores',
                    data:datos,
                    backgroundColor:[
                        'red',
                        'yellow',
                        'blue',
                        'pink'
                    ],
                    borderColor:[
                        'black',
                        'black',
                        'black',
                        'black'
                    ],
                    borderWidth: 1
                }
            ]
        },
        options:{
            legend:{
                display:false
            },
            'onClick': function (event, item){
                index = item[0]["_index"]
                nombre = item[0]["_chart"].data.labels[index]
                votos = item[0]["_chart"].data.datasets[0].data[index]
            }
        }
    })
}

onMount(crearGrafica)
afterUpdate(()=>
chart.update()
)

</script>

<canvas id="miGrafica" width="1" height="1" ></canvas>
<h1>Posición: {index}</h1>
<h1>Nombre: {nombre} <input type="range" bind:value={datos[index]} max="{max}" > </h1>
<h1>Jugadores: {votos}</h1>
<h1>{max}</h1>
<script>
    import Chart from 'chart.js';
    import {onMount, afterUpdate } from 'svelte';
    
    let chart
    let index= 0;
    let nombre= '';
    let votos=0;
    let datos =[12,23,50,21];
    let max = Math.max(...datos);



    function crearGrafica(){

        let miGraf = document.getElementById('miGrafica').getContext("2d");
        chart = new Chart(miGraf,{
            type:'bar',
            data: {
                labels:['Resident evil', 'Uncharted','Red dead redemption','god of war'],
                datasets: [
                    {
                        label: 'Numero de jugadores',
                        data: datos,
                        backgroundColor: [
                            "red",
                            "yellow",
                            "blue",
                            "pink",
                        ],
                        borderColor: [
                            "black",
                            "black",
                            "black",
                            "black"
                        ],
                        borderWidth: 1
                    }
                ]
            },
            options: {
                legend: {
                    display: false
                },
                'onClick': function(event, item){
                    index = item[0]["_index"]
                    nombre = item[0]["_chart"].data.labels[index]
                    votos = item[0]["_chart"].data.datasets[0].data[index]
                }
            }
        })

    }

    onMount(crearGrafica)
    afterUpdate(()=>chart.update())

</script>

<canvas id="miGrafica" width="1" height="1"></canvas>

<h1>Posicion: {index}</h1>
<h1>Nombre: {nombre}
    <input type="range" bind:value={datos[index]} max="{max}" >
</h1>
<h1>Jugadores: {votos}</h1>
<h1>{max}</h1>
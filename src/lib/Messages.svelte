<script lang="ts">
    export let name:string = '';

    function alquilar() {
        alert('Alquilado');
    }
</script>


<div style="background: gray; border-radius: 8px; box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); padding: 16px;">
    <strong>El Aeropuerto de {name} </strong>
    <p>Está disponible</p>	
    <button on:click={alquilar} style="background-color: blue; color: white; padding: 8px 16px; border: none; border-radius: 4px; cursor: pointer;">Alquilar</button>
</div>
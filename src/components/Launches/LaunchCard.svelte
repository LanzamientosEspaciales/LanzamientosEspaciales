<script lang="ts">
  import { type LaunchType } from "./LaunchType";
  const launch: LaunchType = $props();
</script>

<div class={`launch-card ${launch.important ? "importante" : ""}`}>
  <div class="launch-details">
    <h3 class="launch-mission-name">{launch.missionName}</h3>
    <p class="launch-date"><strong>Fecha: </strong>{launch.date}</p>
    <p class="launch-time"><strong>Hora: </strong>{launch.time}</p>
    <p class="launch-vehicle"><strong>Vehículo: </strong>{launch.vehicle}</p>
    <p class="launch-site"><strong>Lugar: </strong>{launch.site}</p>
  </div>
  <img src={launch.img} alt={launch.missionName} class="launch-image" />

  <a href="/" class="btn-ver-mas"> Ver más </a>
</div>

<style lang="scss">
  .launch-card {
    background-color: var(--navy-blue);
    padding: 1.5rem;
    margin: 1.5rem auto;
    width: 80%;
    max-width: 700px;
    border-radius: 1rem;
    box-shadow: 0px 0px 4px var(--cerulean-blue);
    display: flex;
    flex-direction: column;
    transition: transform 0.3s ease-in-out;
    overflow: hidden;
    transition: all 0.25s;

    &.importante {
      box-shadow: 0 0 10px 3px var(--misty-cyan);
    }
  }

  .launch-details {
    text-align: left;
    flex-grow: 1;

    p {
      margin: 0;
    }
  }

  .launch-mission-name {
    font-size: 1.8rem;
    font-weight: bold;
    margin: 0 0 1rem 0;
    text-align: center;
  }

  img {
    width: 100%;
    height: 200px; /* Ajusta la altura según lo que necesites */
    object-fit: cover; /* Asegura que la imagen se recorte y mantenga su proporción */
    border-radius: calc(1rem / 2);
    margin-top: 1rem;
    aspect-ratio: 16/9;
  }
  .btn-ver-mas {
    display: inline-block;
    background-color: var(--midnight-blue);
    font-size: 1rem;
    font-weight: 600;
    padding: 0.6rem 1.5rem;
    border-radius: calc(1rem / 2);
    text-decoration: none;
    text-align: center;
    margin-top: 1rem;
    box-shadow: 0 4px 10px var(--midnight-blue);
    transition: box-shadow 0.125s;

    &:hover {
      box-shadow: 0 0 10px var(--cerulean-blue);
    }
  }
</style>

<script lang="ts">
  import { type LaunchType } from "./LaunchType";
  import LaunchCard from "./LaunchCard.svelte";
  const API_URL: string = "https://controldemision.com/wp-json/eventon/events";

  async function fetchLaunches() {
    let req = await fetch(API_URL).then((res: Response) => res.json());
    let launches: LaunchType[] = Object.values(req["events"])
      .sort((a: any, b: any) => {
        return a["start"] - b["start"];
      })
      .filter((launch: any) => {
        return launch["start"] >= Date.now() / 1000;
      })
      .map((launch: any) => {
        let [vehicle, missionName] = launch["name"].split("•");
        vehicle = vehicle.trim();
        missionName = missionName.trim();

        let dateUTC = new Date(launch["start"] * 1000);
        let date = dateUTC.toLocaleDateString("es-ES");
        let time = dateUTC.toLocaleTimeString("es-ES");

        return {
          missionName,
          date,
          time,
          vehicle,
          site: launch["location_name"] as string,
          img: launch["image_url"] as string,
          important: launch["featured"] == "yes" ? true : false,
        };
      });

    return launches.slice(0, 3);
  }

  let launches: Promise<LaunchType[]> = fetchLaunches();
</script>

<section id="launches" class="border-section">
  <h2>Próximos Lanzamientos</h2>
  <div class="launch-list">
    {#await launches}
      <p>Cargando...</p>
    {:then launches_list}
      {#each launches_list as launch}
        <LaunchCard
          missionName={launch.missionName}
          date={launch.date}
          time={launch.time}
          vehicle={launch.vehicle}
          site={launch.site}
          img={launch.img}
          important={launch.important}
        />
      {/each}
    {:catch e}
      <p>Hubo un error 💔</p>
    {/await}
  </div>
</section>

<style type="scss">
  #launches {
    padding: 2rem;
    text-align: center;
    h2 {
      font-size: 2.5rem;
      margin-bottom: 1rem;
    }
  }

  .launch-list {
    display: flex;
    flex-direction: row;
    gap: 4rem;
    padding: 0 12rem;
  }
</style>

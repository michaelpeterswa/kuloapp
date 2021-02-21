<script>
    import axios from "axios"
    let time= Date.now()/1000 | 0
    let latitude = 47.688357
    let longitude = -120.641625
    let url= "https://cascadelabs.dev/api/predict"
    let resp = "Waiting for submission."

    const handleOnSubmit = () => {
        axios.get(url, {
            params: {
                epoch: time,
                lat: latitude,
                long: longitude,
            }  
        })
        .then((response) => { 
            resp = response.data.acres.toFixed(2) + " acres"
        })
    }
</script>

<form class="content" on:click={handleOnSubmit}>
    <label for="time">Time (epoch)</label>
    <input type="number" id="time" bind:value={time}/>
    <label for="lat">Latitude</label>
    <input type="float" id="lat" bind:value={latitude}/>
    <label for="long">Longitude</label>
    <input type="float" id="long" bind:value={longitude}/>
    <button type="button">
		Submit
	</button>
</form>
<p>{resp}</p>
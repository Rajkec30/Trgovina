<script>
    import { onMount } from 'svelte';
    import axios from 'axios'

    let iname
    let iprice
    let idescription
    let iimgurl

    let name
    let price
    let description
    let imgurl

    let message
    let proizvodi

    let hasp = false


    const getProducts = async () => {
        try {
            let response = await axios.get('https://63149355fc9dc45cb4efbbfb.mockapi.io/api/proizvodi')
            proizvodi = response.data
        } catch (e) {
            console.error('Error')
        }
    }

    const postProduct = async () => {
        if(!imgurl){
            imgurl = 'data:image/jpeg;base64,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'
        }

        if (name){
            if (price) {
                if (description){
                    let allnames = document.querySelectorAll('.proizvodi h1')
                    let result = []

                    allnames.forEach(findName)

                    function findName(pname) {
                        if (pname.innerText === name) {
                            console.log(name)
                            message = "Proizvodi moraju imati razlicito ime!"
                            result.push(pname)
                        }
                    }

                    if (result.length === 0) {
                        await axios.post('https://63149355fc9dc45cb4efbbfb.mockapi.io/api/proizvodi', {
                            name: name,
                            price: price,
                            description: description,
                            imgurl: imgurl,
                        })
                            .then((res) => console.log(res.data))
                            .catch((err) => console.log(err))

                        message = ''
                        name = ''
                        price = ''
                        imgurl = ''
                        description = ''

                        await getProducts()
                    }
                } else {
                    message = 'Proizvod Mora imati Opis'
                }
            } else {
                message = 'Proizvod Mora imati Cijenu!'
            }
        } else {
            message = 'Proizvod Mora imati ime!'
        }
    }

    const deleteProduct = async (id) => {
        await axios.delete(`https://63149355fc9dc45cb4efbbfb.mockapi.io/api/proizvodi/${id}`)
            .then((res) => console.log(res))
            .catch((err) => console.log(err))

        await getProducts()

        if (proizvodi.length < 1) {
            hasp = false
            console.log(proizvodi)
        }
    }

    const seeProduct = (proizvod) => {
        let name = proizvod.name
        let allnames = document.querySelectorAll('h1')
        let result

        allnames.forEach(findName)

        function findName (pname){
            if (pname.innerText === name){
                result = pname
            }
        }

        let div = result.closest('div')
        let desc = div.querySelector('h3')
        let btns = div.querySelectorAll('button')
        let btn = btns[1]

        console.log(div)

        if (desc.style.display === 'block') {
            btn.innerText = 'Pogledaj vise'
            desc.style.display = 'none'
        } else {
            btn.innerText = 'Pogledaj manje'
            desc.style.display = 'block'
        }
    }

    const showEditProduct = (proizvod) => {
        let name = proizvod.name
        let allnames = document.querySelectorAll('h1')
        let result

        allnames.forEach(findName)

        function findName (pname){
            if (pname.innerText === name){
                result = pname
            }
        }

        let div = result.closest('div')
        let btns = div.querySelectorAll('button')
        let btn = btns[2]
        let inputs = div.querySelector('form')

        if (inputs.style.display === 'none'){
            btn.innerText = 'Odustani'
            inputs.style.display = 'block'
        } else {
            btn.innerText = 'Izmjeni'
            inputs.style.display = 'none'
        }

    }

    const editProduct = (id) => {
        axios.put(`https://63149355fc9dc45cb4efbbfb.mockapi.io/api/proizvodi/${id}`, {
            name: iname,
            price: iprice,
            description: idescription,
            imgurl: iimgurl
        })
            .then(() => getProducts())
            .catch((err) => console.log(err))

        iname = ''
        iprice = ''
        idescription = ''
        iimgurl = ''
    }

    onMount( () => {
        getProducts()
    })

    $: if (proizvodi !== undefined){
        if (proizvodi.length > 0){
            hasp = true
        }
    } else{
        hasp = false
    }

</script>

<main>
    {#if proizvodi}
        {#if hasp}
            <div class="proizvodi">
                {#each proizvodi as proizvod}
                    <div class="proizvod">
                        <img src={proizvod.imgurl} alt="" width="200px">
                        <h1>{proizvod.name}</h1>
                        <h3 style="display: none">{proizvod.description}</h3>
                        <h2>{proizvod.price}kn</h2>
                        <form on:submit|preventDefault={editProduct(proizvod.id)} style="display: none">
                            <div class="input-group">
                                <input type="text" bind:value = {iname} placeholder="Ime proizvoda">
                                <input type="number" bind:value = {iprice} placeholder="Cijena (kn)">
                                <input type="text" bind:value = {idescription} placeholder="Opis">
                                <input type="text" bind:value = {iimgurl} placeholder="Url Slike">
                                <button type="submit">Izmjeni</button>
                            </div>
                            <br>
                        </form>
                        <button on:click={seeProduct(proizvod)}>Pogledaj Više</button>
                        <button on:click={showEditProduct(proizvod)}>Izmjeni</button>
                        <button on:click={deleteProduct(proizvod.id)}>Izbrisi</button>
                    </div>
                {/each}
            </div>
        {:else }
            <div class="proizvodi" style="text-align: center">
                <h1>Nema proizvoda, Dodajte Proizvod</h1>
            </div>
        {/if}

        <div class="inputs">
            <h1>Dodaj novi Proizvod</h1>
            <form on:submit|preventDefault={postProduct}>
                <div class="input-group">
                    <input type="text" bind:value = {name} placeholder="Ime proizvoda">
                    <input type="number" bind:value = {price} placeholder="Cijena (kn)">
                    <input type="text" bind:value = {description} placeholder="Opis">
                    <input type="text" bind:value = {imgurl} placeholder="Url Slike">
                    <button type="submit">Dodaj</button>
                    {#if message}
                        <h2>{message}</h2>
                    {/if}
                </div>
            </form>
        </div>
        {:else }
            <div class="loader">
                <img src="images/loader.svg" alt="Loading...">
            </div>
    {/if}
</main>

<style>
    *{
        color: white;
        font-family: Poppins,sans-serif;
    }

    main{
        display: flex;
        gap: 100px;
    }

    input{
        font-size: 13px;
        padding: 5px;
        border: none;
        border-radius: 2px;
        color: #2a2a2a;
        font-weight: 600;
    }

    button{
        cursor: pointer;
        background-color: #c43939;
        border: none;
        border-radius: 2px;
        font-size: 14px;
        padding: 5px;
    }

    .loader{
        position: fixed;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        display: grid;
        place-items: center;
        z-index: 9999;
    }

    .inputs{
        max-width: 50%;
    }

    .proizvodi{
        overflow-y: auto;
        height: 920px;
        display: flex;
        flex-direction: column;
        width: 50%;
        gap: 20px;
        padding-right: 7px;
        border-right: 2px solid white;
    }

    .proizvod{
        background-color: #4d4d4d;
        padding: 20px;
        border-radius: 10px;
    }
</style>
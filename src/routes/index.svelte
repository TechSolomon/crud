<h1>📦 Inventory Tracking</h1>

<script>
    import { CSVDownloader } from 'svelte-csv';

    let headers = ["Item", "Quantity", "Unit Price"]

    // Sample Data
    let inventory = [
        ["Flat Rate Boxes", "37", "$14.99"],
        ["Custom Shipping Labels", "21", "$3.99"],
        ["Biodegradable Packing Peanuts (0.72 lbs / bag)", "14", "$5.95"],
    ]

    let additionalInventoryItem = [...headers]

    function create() {
        inventory = [...inventory, [...additionalInventoryItem]]
        additionalInventoryItem = headers
    }

    function remove(itemType) {
        inventory = inventory.filter(item => item != itemType)
    }
</script>

<table>
    <tr>
        {#each headers as header}
            <th>{header}</th>
        {/each}
    </tr>

    {#each inventory as item}
        <tr>
            {#each item as entry}
                <td contenteditable="true" bind:innerHTML={entry} />
            {/each}
            <button on:click={() => remove(item)}>
                🗑
            </button>
        </tr>
    {/each}

    <tr class="add">
        {#each additionalInventoryItem as header}
            <td contenteditable="true" bind:innerHTML={header} />
        {/each}

        <button on:click={create}>
            ➕
        </button>
    </tr>
</table>

<div class='selection'>
    <CSVDownloader data={[headers, inventory[0], inventory[1], inventory[2]]} type={'button'} filename={'inventory-tracking'} bom={true}>
        🚀 CSV
    </CSVDownloader>
</div>
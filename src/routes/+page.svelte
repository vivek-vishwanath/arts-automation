<script>

	let filterIndex = 1;
	let filterText = ""
	let filterOptions = ["Environment Name", "Access Name", "Description", "Protected By"]
	let rows = [];
	for (let i = 0; i < 17; i++) {
		rows.push({ id: i + 1, selected: false, environmentName: "test_env_1", accessName: "ACCESS_GROUP_" + i, description: "GENERIC_DESCRIPTION_" + i, protectedBy: "IG_JAKE_FROM_SF", businessCase: '' });
	}
	shuffle(rows)
	let r2 = []
	for (let i = 0; i < 31; i++) {
		r2.push({ id: i + 18, selected: false, environmentName: "test_env_2", accessName: "ACCESS_GROUP_" + i, description: "SAMPLE_DESCRIPTION_" + i, protectedBy: "IG_JAKE_FROM_SF", businessCase: '' });
	}

	shuffle(r2)
	for (let i = 0; i < 31; i++) {
		rows.push(r2[i]);
	}

	shuffle(rows)

	let showBusinessCase = false;

	let showPopup = false;

	function shuffle(array) {
		for (let i = array.length - 1; i > 0; i--) {
			const j = Math.floor(Math.random() * (i + 1));
			[array[i], array[j]] = [array[j], array[i]];
		}
		return array;
	}

	function apply() {
		showPopup = true;
	}

	function gotoBusinessCase() {
		showBusinessCase = true;
	}

	function goBack() {
		showBusinessCase = false;
	}

	function closePopup() {
		showPopup = false;
	}

	function renewAccesses() {
		showPopup = false;
	}

	function showRow(text, index, row, businessCase) {
		let filters = [row.environmentName, row.accessName, row.description, row.protectedBy];
		return (!businessCase || row.selected) && filters[index].toLowerCase().includes(text.toLowerCase());
	}

</script>

<style>
    :global(body) {
        font-family: 'Verdana', sans-serif;
        margin: 0;
        background-color: #f7f7f7;
    }

    .banner {
        /*text-align: center;*/
        background-color: #e74c3c;
        color: white;
        padding: 0.7em;
        font-size: 2.5em;
				font-style: italic;
				font-family: "Trebuchet MS", sans-serif;
        border-bottom: 3px solid #c0392b;
    }

    .container {
        display: flex;
        flex-direction: column;
        align-items: center;
        /*justify-content: center;*/
        margin-top: 32px;
        max-height: 384px; /* Adjust the height as needed */
        overflow-y: auto;
    }

    .apply {
        display: flex;
        justify-content: center;
        margin-top: 16px;
    }

    .column-headers {
        font-family: "Trebuchet MS", sans-serif;
    }

    .bottom-buttons {
        font-family: "Trebuchet MS", sans-serif;
        margin: 16px;
    }

    table {
        border-collapse: collapse;
        width: 80%;
        margin-bottom: 1em;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        background-color: white;
        border-radius: 8px;
        overflow: hidden;
    }

    th, td {
        border: none;
        padding: 12px 15px;
        text-align: left;
    }

    th {
        background-color: #e74c3c;
        color: white;
    }

    .selected {
        background-color: #fdecec;
    }

    tr:hover {
        background-color: #eaf2f8;
    }

    button {
        background-color: #e74c3c;
        color: white;
        padding: 10px 20px;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        font-size: 1em;
        transition: background-color 0.3s ease;
    }

    button:hover {
        background-color: #c0392b;
    }

    .popup {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: rgba(0, 0, 0, 0.5);
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .popup-content {
        background: white;
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }

    .popup-title {
        font-size: large;
        justify-content: center;
        display: flex;
    }

    .close {
        margin-top: 10px;
        cursor: pointer;
        color: #e74c3c;
        background: none;
        border: none;
        font-size: 1em;
        padding: 10px;
        border-radius: 5px;
        transition: background-color 0.3s ease;
    }

    .close:hover {
        background-color: #fdecec;
    }

    /* Customize the checkbox */
    .custom-checkbox {
        display: inline-block;
        position: relative;
        padding-left: 30px; /* Adjust the padding as needed */
        margin-right: 15px; /* Adjust the margin as needed */
        height: 15px;
        cursor: pointer;
        user-select: none;
    }

    /* Hide the default checkbox */
    .custom-checkbox input {
        position: absolute;
        opacity: 0;
        cursor: pointer;
    }

    /* Style the checkmark */
    .checkmark {
        position: absolute;
        top: 0;
        left: 0;
        height: 20px; /* Adjust the height as needed */
        width: 20px; /* Adjust the width as needed */
        background-color: #ccc; /* Checkbox background color */
        border-radius: 20%; /* Rounded corners */
    }

    /* On hover, add a background color to the checkmark */
    .custom-checkbox:hover input ~ .checkmark {
        background-color: #bbb;
    }

    /* When the checkbox is checked, change the checkmark color */
    .custom-checkbox input:checked ~ .checkmark {
        background-color: #2196F3; /* Your preferred checked color */
    }

    /* Create the checkmark inside the checkbox */
    .checkmark:after {
        content: "";
        position: absolute;
        display: none;
    }

    /* Show the checkmark when the checkbox is checked */
    .custom-checkbox input:checked ~ .checkmark:after {
        display: block;
    }

    /* Style the checkmark itself */
    .custom-checkbox .checkmark:after {
        left: 8px; /* Adjust the position as needed */
        top: 2px; /* Adjust the position as needed */
        width: 3px; /* Adjust the width as needed */
        height: 10px; /* Adjust the height as needed */
        border: solid #fff; /* Checkmark color */
        border-width: 0 3px 3px 0; /* Checkmark shape */
        transform: rotate(45deg); /* Rotate the checkmark */
    }

    .form-field {
        display: flex;
        flex-direction: column;
				width: 384px;
        margin: 1rem 2rem 1rem 0;
    }

    .form-label {
        font-weight: bold;
        margin-bottom: 0.5rem;
    }

    .form-input {
        padding: 0.75rem;
        border: 2px solid #ddd;
        border-radius: 8px;
        font-size: 1rem;
        transition: border-color 0.3s;
    }

    .form-input:focus {
        border-color: #007BFF;
        outline: none;
    }

		.access-name-search {
				margin-top: 32px;
				margin-left: 16px;
				width: 256px;
		}

		.search-icon {
				width: 24px;
				height: 24px;
				margin-left: 8px;
		}

    /* Dropdown container */
    .dropdown {
        position: relative;
        display: inline-block;
        margin-left: 152px;
    }

    /* Dropdown button */
    .dropbtn {
        background-color: #3498db;
        color: white;
        padding: 10px;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }

    /* Dropdown content (hidden by default) */
    .dropdown-content {
        display: none;
        position: absolute;
        background-color: #f9f9f9;
        /*min-width: 160px;*/
        border-radius: 5px;
        box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
        z-index: 1;
    }

    /* Links inside the dropdown */
    .dropdown-content a {
        color: black;
        padding: 12px 16px;
        text-decoration: none;
        display: block;
    }

    /* Change background color of dropdown links on hover */
    .dropdown-content a:hover {
        background-color: #f1f1f1;
    }

    /* Show the dropdown menu on hover */
    .dropdown:hover .dropdown-content {
        display: block;
    }

		.dropdown-item {
				border-radius: 0;
				width: 100%;
		}

		.last {
				border-bottom-left-radius: 8px;
        border-bottom-right-radius: 8px;
		}

</style>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">

<div class="banner">Lost Access</div>
<div>
	<div class="dropdown">
		<button class="btn"><i class="fa fa-filter"></i> {filterOptions[filterIndex]}</button>
		<div class="dropdown-content">
			<button class="dropdown-item" on:click={() => {filterIndex = 0}}>Environment Name</button>
			<button class="dropdown-item" on:click={() => {filterIndex = 1}}>Access Name</button>
			<button class="dropdown-item" on:click={() => {filterIndex = 2}}>Description</button>
			<button class="dropdown-item last" on:click={() => {filterIndex = 3}}>Protected By</button>
		</div>
	</div>
	<input
		class="access-name-search form-input"
		style="font-size: small"
		bind:value={filterText}
		placeholder={filterOptions[filterIndex]}
	/>
	<img src="search.png" alt="search" class="search-icon"/>
</div>
<div class="container">
	<table>
		<thead>
		<tr class="column-headers">
			{#if !showBusinessCase}
				<th>Renew?</th>
			{/if}
			<th>Environment Name</th>
			<th>Access Name</th>
			<th>Description</th>
			<th>Protected by</th>
			{#if showBusinessCase}
				<th>Business Case</th>
			{/if}
		</tr>
		</thead>
		<tbody>
		{#each rows as row (row.id)}
			{#if showRow(filterText, filterIndex, row, showBusinessCase) }
				<tr class:selected={row.selected}>
					{#if !showBusinessCase}
						<td>
							<label class="custom-checkbox">
								<input type="checkbox" bind:checked={row.selected} on:change={() => {}} />
								<span class="checkmark"></span>
							</label>
						</td>
					{/if}
					<td>{row.environmentName}</td>
					<td>{row.accessName}</td>
					<td>{row.description}</td>
					<td>{row.protectedBy}</td>
					{#if showBusinessCase}
						<div class="form-field">
							<input
								class="form-input"
								style="font-size: x-small"
								bind:value={row.businessCase}
								placeholder="As a software engineer, I would need this access to perform my responsibilities."
							/>
						</div>

					{/if}
				</tr>
			{/if}
		{/each}
		</tbody>
	</table>
</div>
<div class="apply">
	{#if showBusinessCase}
		<button class="bottom-buttons" on:click={goBack}>Back</button>
	{/if}

	<button class="bottom-buttons" on:click={showBusinessCase ? apply : gotoBusinessCase}>Renew</button>
</div>

{#if showPopup}
	<div class="popup">
		<div class="popup-content">
			<p class="popup-title">Are you sure you want to renew {rows.filter(row => row.selected).length} access
				requests?</p>

			<div class="container">
				<table>
					<thead>
					<tr class="column-headers">
						<th>Environment Name</th>
						<th>Access Name</th>
						<th>Description</th>
						<th>Protected by</th>
						<th>Business Case</th>
					</tr>
					</thead>
					<tbody>
					{#each rows as row (row.id)}
						{#if row.selected}
							<tr class:selected={row.selected}>
								<td>{row.environmentName}</td>
								<td>{row.accessName}</td>
								<td>{row.description}</td>
								<td>{row.protectedBy}</td>
								<p style="margin-right: 8px; width: 300px; word-wrap: break-word">{row.businessCase}</p>
							</tr>
						{/if}
					{/each}
					</tbody>
				</table>
			</div>
			<div style="display: flex; justify-content: flex-end">
				<button class="close" on:click={renewAccesses}>Yes</button>
				<button class="close" on:click={closePopup}>No</button>
			</div>
		</div>
	</div>
{/if}

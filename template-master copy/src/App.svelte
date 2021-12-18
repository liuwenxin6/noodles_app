<script>
	class Noodle{
	// text: string
	// firm_time: number
	// avg_time : number
	// soft_time: number

		constructor (name, firm_input, avg_input, soft_input){
		this.text = name;
		this.firm_time = firm_input;
		this.avg_time = avg_input;
		this.soft_time = soft_input;
		}
	}
	
	let selected;

	let cook_time = '';
	let default_nood = [ 
		new Noodle("Acini de pepe", 4,5,6 ),
		new Noodle("Capellini",4,5,6),
		new Noodle("Elbow macaroni",8,9,10),
		new Noodle("Farfalle",13,14,15),
		new Noodle("Fettuccine",11,12,13),
		new Noodle("Fusilli",11,12,13),
		new Noodle("Lasagna noodles",12,14,15),
		new Noodle("Linguine",9,11,13),
		new Noodle("Mafalda",8,9,10),
		new Noodle("Manicotti",10,11,12),
		new Noodle("Mostaccioli",12,13,14),
		new Noodle("Penne",7,11,13),
		new Noodle("Radiatore",9,10,11),
		new Noodle("Rigatoni",12,14,15),
		new Noodle("Rotelle",10,11,12),
		new Noodle("Rotini",8,9,10),
		new Noodle("Spaghetti",8,9,10),
		new Noodle("Vermicelli",5,6,7),
		new Noodle("Wagon wheel",10,11,12),
		new Noodle("Ziti",13,14,15)
	]
	let Noodles = [
		new Noodle("New noodle name")
	]

	const add_Noodle = () => {
		Noodles = Noodles.concat([new Noodle("New Noodle Name")])
	}
	

	const delete_Noodle = (Noodle_to_delete) => {
		if (confirm = "Delete " + Noodle_to_delete.text + "?"){
			Noodles = Noodles.filter((Noodle) => Noodle != Noodle_to_delete)
		}
	}

	function compute_time() {
		let n_name = (document.getElementById("selected_noodle")).value
		
		let cookedness_wanted = document.forms.theForm.elements.cookedness.value
		let cookedness_str = cookedness_wanted

		let huge_noodle_list = default_nood.concat(Noodles)
		let target_noodle = (huge_noodle_list.filter((Noodle) => Noodle.text == n_name))[0]
		if (cookedness_str == "firm_wanted"){
			cook_time = target_noodle.firm_time
		}
		else if (cookedness_str == "avg_wanted"){
			cook_time = target_noodle.avg_time
		}
		else{
			cook_time = target_noodle.soft_time
		}
	}

</script>

<style>
	h1{
		color: green;
		text-align: center;
		font-family: Arial, Helvetica, sans-serif;
	}
	todo-Noodle{
		border: 1px solid green;
		padding: 10px;
		border-radius: 5px;

		width: 500px;
		box-sizing: border-box;
		
		display: grid;
		grid-template:
			" textfield delete_button" 
		/ auto 1fr
	}

	button{
		background-color: green;
		color: white;
		border: 1px solid green;
		padding: 10px;
		border-radius: 5px;

		font-weight: bold;
		max-width: 500px;
		
	}
</style>

<h1> PASTA COOK TIME APP</h1> 
Note: start timing your pasta for the recommended time (in minutes) after you've thrown in your pasta into the boiling water as a normal person does.
<form name= "theForm">
	<select value={selected} id = "selected_noodle">

		<option value = "tes"> Select types of noodles here </option>
		{#each default_nood as user}
			<option value = {user.text}> {user.text} </option>
		{/each}
		{#each Noodles as user}
			<option value = {user.text}> {user.text} </option>
		{/each}
	</select>
	
	<label>
	<input type = radio name = "cookedness" value = "firm_wanted">
	 Firm</label>

	<label>
	<input type = radio name = "cookedness" value = "avg_wanted">
	Avg</label>

	<label>
	<input type = radio name = "cookedness" value = "soft_wanted">
	 Soft</label>

	<button  type=submit on:click = {compute_time}>
		Compute
	</button>
</form>

Your cook time should be: {cook_time}

{#each Noodles as Noodle}
<todo-Noodle  >
	Name of noodles:
	<input type = "text" bind:value = {Noodle.text}/>
	Time for firm:
	<input type = "number" min =1  bind:value = {Noodle.firm_time}/>
	Time for avg:
	<input type = "number" min =1 bind:value = {Noodle.avg_time}/>
	Time for soft:
	<input type = "number" min =1 bind:value = {Noodle.soft_time}/>
	<button on:click = {() => delete_Noodle(Noodle)}> X </button>
</todo-Noodle>
{/each}
<button on:click = {add_Noodle}>  ADD PASTA</button>

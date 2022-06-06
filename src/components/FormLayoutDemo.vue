<template>
	<div class="grid">
		<!--<div class="col-12 md:col-6">
			<div class="card p-fluid">
				<h5>Vertical</h5>
				<div class="field">
					<label for="name1">Name</label>
					<InputText id="name1" type="text" />
				</div>
				<div class="field">
					<label for="email1">Email</label>
					<InputText id="email1" type="text" />
				</div>
				<div class="field">
					<label for="age1">Age</label>
					<InputText id="age1" type="text" />
				</div>
			</div>

			<div class="card p-fluid">
				<h5>Vertical Grid</h5>
				<div class="formgrid grid">
					<div class="field col">
						<label for="name2">Name</label>
						<InputText id="name2" type="text" />
					</div>
					<div class="field col">
						<label for="email2">Email</label>
						<InputText id="email2" type="text" />
					</div>
				</div>
			</div>
		</div>

		<div class="col-12 md:col-6">
			<div class="card p-fluid">
				<h5>Horizontal</h5>
				<div class="field grid">
					<label for="name3" class="col-12 mb-2 md:col-2 md:mb-0">Name</label>
					<div class="col-12 md:col-10">
						<InputText id="name3" type="text" />
					</div>
				</div>
				<div class="field grid">
					<label for="email3" class="col-12 mb-2 md:col-2 md:mb-0">Email</label>
					<div class="col-12 md:col-10">
						<InputText id="email3" type="text" />
					</div>
				</div>
			</div>

			<div class="card">
				<h5>Inline</h5>
				<div class="formgroup-inline">
					<div class="field">
						<label for="firstname1" class="p-sr-only">Firstname</label>
						<InputText id="firstname1" type="text" placeholder="Firstname"/>
					</div>
					<div class="field">
						<label for="lastname1" class="p-sr-only">Lastname</label>
						<InputText id="lastname1" type="text" placeholder="Lastname"/>
					</div>
					<Button label="Submit"></Button>
				</div>
			</div>

			<div class="card">
				<h5>Help Text</h5>
				<div class="field p-fluid">
					<label for="username">Username</label>
					<InputText id="username" type="text" />
					<small>Enter your username to reset your password.</small>
				</div>
			</div>
		</div>-->

		<div class="col-12">
			<div class="card">
				<h5>Arama Kriterleri</h5>
				<div class="p-fluid formgrid grid">
					<div class="field col-12 md:col-6">
						<label for="invoiceNo">Fatura No</label>
						<InputText id="invoiceNo" type="text"/>
					</div>
					<div class="field col-12 md:col-6">
						<label for="vendorName">Tedarikci Adı</label>
						<InputText id="vendorName" type="text"/>
					</div>
					<div class="field col-12">
						<label for="vkn">Vkn</label>
						<InputText id="vkn" type="text"/>
					</div>
					<div class="field col-12 md:col-6">
						<label for="rangeDate">Tarih Aralığı</label>
						<Calendar v-model="rangeDate" selectionMode="range" />	
					</div>
					<div class="field col-12 md:col-3">
						<label for="status">Statü</label>
						<Dropdown id="status" v-model="dropdownItem" :options="dropdownItems" optionLabel="name" placeholder="Seçiniz"></Dropdown>
					</div>
					<div class="field col-12 md:col-3">
						<label for="ettn">Ettn</label>
						<InputText id="ettn" type="text"/>
					</div>
					<div class="field col-12 md:col-3">
					<Button type="button" label="Sonuçları Filtrele" @click="filter" aria-haspopup="true" aria-controls="overlay_menu"/>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				dropdownItems: [
					{name: 'Faturalandı', code: 'Option 1'},
					{name: 'Beklemede', code: 'Option 2'},
					{name: 'Kaldirildi', code: 'Option 3'}
				],
				dropdownItem: null,
				rangeDate : null
			}
		},
		methods: {
			filter() {
            //this.$refs.menu.toggle(event);
			this.$router.push({ name: 'list' })
        }
		}
	}
</script>

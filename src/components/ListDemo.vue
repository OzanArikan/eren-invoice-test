<template>
	<div class="grid">
		<div class="col-12">
			<div class="card">
			<Toast />
				<h5>Gelen Faturalar</h5>
				<DataView :value="dataviewValue" :layout="layout" :paginator="true" :rows="10" :sortOrder="sortOrder"
					:sortField="sortField" :lazy="true">
					<template #header>
						<div class="grid grid-nogutter">
							<!--<div class="col-6 text-left">
							<label for="sort">Fiyata Göre</label>
								<Dropdown v-model="sortKey" :options="sortOptions" optionLabel="label"
									placeholder="Sort By Price" @change="onSortChange($event)" />
							</div>
							<div class="col-6 text-left">
							<label for="range">Tarihe Göre</label>
								<Calendar v-model="rangeDate" selectionMode="range" />	
							</div>-->
							<!--<div class="col-6 text-right">
								<DataViewLayoutOptions v-model="layout" />
							</div>-->
							<!--<Menu id="overlay_menu" ref="menu" :model="menuItems" :popup="true" />-->
							<Button type="button" label="Filtrele" @click="toggle" aria-haspopup="true"
								aria-controls="overlay_menu" />
						</div>
					</template>
					<!--<template #list="slotProps">
						<div class="col-12">
							<div class="flex flex-column md:flex-row align-items-center p-3 w-full">
								<img :src="'images/product/' + slotProps.data.image" :alt="slotProps.data.name" class="my-4 md:my-0 w-9 md:w-10rem shadow-2 mr-5" />
								<div class="flex-1 text-center md:text-left">
									<div class="font-bold text-sm">{{ slotProps.data.name }}</div>
									<div class="mb-3">{{ slotProps.data.description }}</div>
									<Rating :modelValue="slotProps.data.rating" :readonly="true" :cancel="false"
										class="mb-2"></Rating>
									<div class="flex align-items-center">
										<i class="pi pi-tag mr-2"></i>
										<span class="font-semibold">{{ slotProps.data.category }}</span>
									</div>

								</div>
								<div
									class="flex flex-row md:flex-column justify-content-between w-full md:w-auto align-items-center md:align-items-end mt-5 md:mt-0">
									<span
										class="text-sm font-semibold mb-2 align-self-center md:align-self-end">${{ slotProps.data.price }}</span>
									<Button icon="pi pi-shopping-cart" label="Add to Cart"
										:disabled="slotProps.data.inventoryStatus === 'OUTOFSTOCK'"
										class="mb-2"></Button>
									<span
										:class="'product-badge status-' + slotProps.data.inventoryStatus.toLowerCase()">{{ slotProps.data.inventoryStatus }}</span>
								</div>
							</div>
						</div>
					</template>-->

					<template #grid="slotProps">
						<div class="col-12 md:col-4">
							<div class="card m-3 border-1 surface-border">
								<div class="flex align-items-center justify-content-between">
									<div class="flex align-items-center">
										<i class="pi pi-tag mr-2"></i>
										<span class="font-semibold">{{ slotProps.data.category }}</span>
									</div>
									<span
										:class="'product-badge status-' + slotProps.data.inventoryStatus.toLowerCase()">{{
												slotProps.data.inventoryStatus
										}}</span>
								</div>
								<div class="text-center">
									<!--<img :src="'images/product/' + slotProps.data.image" :alt="slotProps.data.name" class="w-9 shadow-2 my-3 mx-0"/>-->
									<div class="text-sm font-bold">{{ slotProps.data.name }}</div>
									<div class="mb-3">{{ slotProps.data.description }}</div>
									<div class="mb-3">{{ slotProps.data.invoiceDate }}</div>
									<!--
									<Rating :modelValue="slotProps.data.rating" :readonly="true" :cancel="false">
									</Rating>-->
								</div>
								<div class="flex align-items-center justify-content-center">
								<p></p>
									<Dialog header="Karar" v-model:visible="display" :breakpoints="{ '960px': '75vw' }"
										:style="{ width: '30vw' }" :modal="true">
										<div class="p-fluid formgrid grid">
											<Dropdown v-model="selectedCountry" :options="countries" optionLabel="name"
												:filter="true" placeholder="Atanan Kişi Seçiniz" :showClear="true">
											</Dropdown>
										</div>
										<template #footer>
											<Button label="Ok" @click="close" icon="pi pi-check"
												class="p-button-outlined" />
										</template>
									</Dialog>
									<!--<span class="text-sm font-semibold">${{slotProps.data.price}}</span>-->
									<Button icon="pi pi-check-circle" style="background-color: green"
										:disabled="slotProps.data.inventoryStatus === 'OUTOFSTOCK'"
										@click="open"></Button>
									<Button icon="pi pi-times-circle" style="background-color: red"
										:disabled="slotProps.data.inventoryStatus === 'OUTOFSTOCK'"
										@click="open"></Button>
									<Button icon="pi pi-paperclip" style="background-color: blue"
										:disabled="slotProps.data.inventoryStatus === 'OUTOFSTOCK'"
										@click="load(3)"></Button>
								</div>
							</div>
						</div>
					</template>
				</DataView>
			</div>
		</div>

		<!--<div class="col-12 lg:col-8">
			<div class="card">
				<h5>PickList</h5>
				<PickList v-model="picklistValue" listStyle="height:250px" dataKey="code">
					<template #sourceheader>
						From
					</template>
					<template #targetheader>
						To
					</template>
					<template #item="slotProps">
						<div>{{slotProps.item.name}}</div>
					</template>
				</PickList>
			</div>
		</div>-->

		<!--<div class="col-12 lg:col-4">
			<div class="card">
				<h5>OrderList</h5>
				<OrderList v-model="orderlistValue" listStyle="height:250px" dataKey="code" :rows="10">
					<template #header>
						Cities
					</template>
					<template #item="slotProps">
						<div>{{slotProps.item.name}}</div>
					</template>
				</OrderList>
			</div>
		</div>-->
	</div>
</template>

<script>
//import ProductService from "../service/ProductService";;

import InvoiceService from "../service/InvoiceService";

export default {
	data() {
		return {
			picklistValue: [[
				{ name: 'San Francisco', code: 'SF' },
				{ name: 'London', code: 'LDN' },
				{ name: 'Paris', code: 'PRS' },
				{ name: 'Istanbul', code: 'IST' },
				{ name: 'Berlin', code: 'BRL' },
				{ name: 'Barcelona', code: 'BRC' },
				{ name: 'Rome', code: 'RM' },
			], []],
			orderlistValue: [
				{ name: 'San Francisco', code: 'SF' },
				{ name: 'London', code: 'LDN' },
				{ name: 'Paris', code: 'PRS' },
				{ name: 'Istanbul', code: 'IST' },
				{ name: 'Berlin', code: 'BRL' },
				{ name: 'Barcelona', code: 'BRC' },
				{ name: 'Rome', code: 'RM' },
			],
			dataviewValue: null,
			layout: 'grid',
			sortKey: null,
			sortOrder: null,
			sortField: null,
			sortOptions: [
				{ label: 'Price High to Low', value: '!price' },
				{ label: 'Price Low to High', value: 'price' },
			],
			rangeDate: null,
			loading: [false, false, false],
			menuItems: [
				{
					label: 'Update',
					icon: 'pi pi-refresh',
					command: () => {
						this.$toast.add({ severity: 'success', summary: 'Updated', detail: 'Data Updated', life: 3000 });
					}
				},
				{
					label: 'Delete',
					icon: 'pi pi-times',
					command: () => {
						this.$toast.add({ severity: 'warn', summary: 'Delete', detail: 'Data Deleted', life: 3000 });
					}
				},
				{
					label: 'Vue Website',
					icon: 'pi pi-external-link',
					url: 'https://vuejs.org/'
				},
				{
					label: 'Router',
					icon: 'pi pi-upload',
					to: '/fileupload'
				}
			],
			display: false,
			countries: [
                {name: 'Hasan', code: 'HERO5'},
                {name: 'Emre', code: 'HEROT'},
                {name: 'Ayşe', code: 'HER06'},
                {name: 'Hakan', code: 'EG'},
                {name: 'Hatice', code: 'FR'},
                {name: 'Germany', code: 'DE'},
                {name: 'India', code: 'IN'},
                {name: 'Japan', code: 'JP'},
                {name: 'Spain', code: 'ES'},
                {name: 'United States', code: 'US'}
            ],
			messages: []
		}
	},
	//productService: null,
	invoiceService: null,
	created() {
		//this.productService = new ProductService();
		this.invoiceService = new InvoiceService();
	},
	mounted() {
		//this.productService.getProducts().then(data => this.dataviewValue = data);
		this.invoiceService.getInvoices().then(data => this.dataviewValue = data);
	},
	methods: {
		onSortChange(event) {
			const value = event.value.value;
			const sortValue = event.value;

			if (value.indexOf('!') === 0) {
				this.sortOrder = -1;
				this.sortField = value.substring(1, value.length);
				this.sortKey = sortValue;
			}
			else {
				this.sortOrder = 1;
				this.sortField = value;
				this.sortKey = sortValue;
			}
		},
		load(index) {
			//this.loading[index] = true;
			//setTimeout(() => this.loading[index] = false, 1000);
			//alert("Bastin" + index);
			if (index === 1) this.$router.push({ name: 'overlay' })
			if (index === 2) this.$router.push({ name: 'overlay' })
			if (index === 3) this.$toast.add({severity:'success', summary: 'Bilgi', detail:'Fatura görüntüsü hazırlanıyor', life: 5000});
		},
		toggle() {
			//this.$refs.menu.toggle(event);
			this.$router.push({ name: 'formlayout' })
		},
		open() {
			this.display = true;
		},
		close() {
			this.display = false;
		},
	}
}
</script>

<style scoped lang="scss">
@import '../assets/demo/badges.scss';


</style>

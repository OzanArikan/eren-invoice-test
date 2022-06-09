<template>
    <!--<div class="surface-0 flex align-items-center justify-content-center min-h-screen min-w-screen overflow-hidden">-->
        <div class="grid justify-content-center p-2 lg:p-0" style="min-width:80%">
            <!--<div class="col-12 md:col-6 mt-5 xl:mt-0 text-center">
                <img :src="'layout/images/logo-' + logoColor + '.svg'" alt="Sakai logo" class="mb-5" style="width:81px; height:60px;">
            </div>-->
            
            <!--<div class="col-12 xl:col-6" style="border-radius:56px; padding:0.3rem; background: linear-gradient(180deg, var(--primary-color), rgba(33, 150, 243, 0) 30%);">-->
                <div class="h-full w-full m-0 py-7 px-4" style="border-radius:53px; ">
                    <div class="text-center mb-5">
                        <!--<img src="layout/images/avatar.png" alt="Image" height="50" class="mb-3">-->
                        <img alt="Logo" :src="topbarImage()" style= "size: 0.5rem;"/>
                         <div class="text-900 text-3xl font-medium mb-3"></div>
                        <span class="text-600 font-medium"> Giriş Yapınız </span>
                    </div>
                
                    <div class="w-full md:w-6 mx-auto">
                        <label for="email1" class="block text-900 text-xl font-medium mb-2">Kullanıcı Adı</label>
                        <InputText id="email1" v-model="email" type="text" class="w-full mb-3" placeholder="Email" style="padding:1rem;" />
                
                        <label for="password1" class="block text-900 font-medium text-xl mb-2">Şifre</label>
                        <Password id="password1" v-model="password" placeholder="Şifre" :feedback="false"  :toggleMask="true" class="w-full mb-3" inputClass="w-full" inputStyle="padding:1rem"></Password>
                      
                        <label for="company" class="block text-900 text-xl font-medium mb-2">Şirket</label>
                        <div class="p-fluid mb-5">
                        <Dropdown v-model="selectedCompany" :options="companies" optionLabel="name"
												:filter="true" placeholder="Şirket Seçiniz" :showClear="true">
											</Dropdown>
                        </div>
                        <div class="flex align-items-center justify-content-between mb-5">
                            <div class="flex align-items-center">
                                <Checkbox id="rememberme1" v-model="checked" :binary="true" class="mr-2"></Checkbox>
                                <label for="rememberme1">Hatırla Beni</label>
                            </div>
                            <a class="font-medium no-underline ml-2 text-right cursor-pointer" style="color: var(--primary-color)">Şifremi Unuttum?</a>
                        </div>
                        <Button label="Giriş" class="w-full p-3 text-xl" :loading="loading[3]" @click="load(3)" ></button>
                    </div>
                </div>
            </div>
        <!--</div>-->
   <!-- </div>-->
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            checked: false,
            selectedCompany : null,
            companies: [
                {name: 'Erde Pazarlama ', code: '104'},
                {name: 'Devanlay', code: '105'},
                {name: 'Modern Dış Ticaret', code: '106'},
                {name: 'Eren Perakende', code: '4726'},
                {name: 'Ganter', code: '4825'},
                {name: 'Dust Street', code: '9214'},
                {name: 'Erkops', code: '9825'},
                {name: 'EPR Tekstil', code: '4726'}
            ],
            loading: [false, false, false]
        }
    },
    computed: {
        logoColor() {
            if (this.$appState.darkTheme) return 'white';
            return 'dark';
        }
    },methods :{
        topbarImage() {
			return 'images/eren.jpg'
			//return this.$appState.darkTheme ? 'images/logo-white.svg' : 'images/logo-dark.svg';
		},
        signIn(){
           this.$router.push({ name: 'list' })
        },
        load(index) {
            this.loading[index] = true;
            setTimeout(
                  () => {this.loading[index] = false
                  this.$router.push({ name: 'list' })} 
                  , 3000);
            
        }
    }
}
</script>

<style scoped>
.pi-eye {
    transform:scale(1.6);
    margin-right: 1rem;
}

.pi-eye-slash {
    transform:scale(1.6);
    margin-right: 1rem;
}
</style>
<template>
	<div class="home">
			<!-----Mobile Design------>
		<div class="container md:hidden">
			<div class="template bg-indigo-900 w-full h-64 fixed">
				<div class="bg-indigo-900 mt-20">
					<img src="../assets/bg-card-back.png" class="w-64 mt-10 h-32 mx-24 ">
					<p class="pad text-white text-lg absolute">{{cardValue}}</p>
					<div>
						<img src="../assets/bg-card-front.png" class="w-68 -mt-12 h-40 mx-4 absolute">
						<img src="../assets/card-logo.svg" class="w-9 h-5 absolute mx-9 -mt-9">
						<span class="text absolute mx-14 mt-6 text-white ">{{ cardNumber }}</span>
					</div>
					<div class="flex justify-between">
							<h3 class="field absolute mt-20 text-white mx-16 text-sm font-semibold">{{ cardName }}</h3>

							<h3 class="fields absolute mt-20 text-white  font-semibold">{{date}}</h3>
					</div>
				</div>

				<teleport to="#modal">
					<div v-if="isShowing">
						<Modal />
					</div>
				</teleport>
				
				<form @submit.prevent="showForm" v-if="!isShowing">
					<div class="container flex justify-center">
						<label class="card absolute mt-40 ">CARDHOLDER NAME</label>
						<input type="text" placeholder=" e.g. Jane Appleseed" class="mt-48 px-3 border-2 rounded border-slate-300 w-10/12 py-1"  v-model="cardName">
						
					</div>
					<div class="container flex justify-center">
						<label class="cards absolute mt-4">CARD NUMBER</label>
						<input type="number" placeholder=" e.g. 1234 5678 9123 0000" class="mt-11 border-2 rounded border-slate-300 px-3  w-10/12 py-1" v-model="cardNumber">
						
					</div>
					<div class="grid grid-cols-3">
						<div class="mt-4 ml-9">
							<label >EXP. DATE</label>
							<input type="number" placeholder="MM" class="border-2 rounded border-slate-300 px-1 h-8 w-14" v-model="date">
							
						</div>
						<div class="mt-4 mx-5">
							<label >(MM/YY)</label>
							<input type="text" placeholder="YY" class="border-2 rounded border-slate-300 px-1 h-8 w-14" v-model="year">
							
						</div>
						<div class="mt-4">
							<label >CVC</label>
							<input type="number" placeholder="e.g. 123" class="border-2 rounded border-slate-300 h-9 w-28 absolute mt-6 px-1 -mx-10" v-model="cardValue" >
						</div>
					</div>
					<button class="block mx-auto bg-indigo-900 mt-7 text-sm text-white py-2 text-lg font-bold tracking-wide w-[380px] rounded">
						Confirm
					</button>
					<p>{{errors}}</p>
				</form>
			</div>
		</div>

			<!-----Screen Design------>
			<div class="container md:flex hidden">
				<div>
					<div class="grid grid-cols-2">
						<div class="bg-indigo-900 w-96 h-screen">
							<img src="../assets/bg-card-front.png" class="w-68 mt-32 h-40 mx-44 absolute">
							<img src="../assets/card-logo.svg" class="w-12 h-7 absolute mx-48 mt-36">
							<span class="text absolute mx-56 mt-52 text-white">{{cardNumber}}</span>
							<div class="flex justify-between">
								<h3 class="font absolute mt-64 mx-48 text-sm font-semibold text-white">{{cardName}}</h3>

								<h3 class="fonts absolute mt-64   font-semibold text-white">{{date}}</h3>
								<div>
									<img src="../assets/bg-card-back.png" class="img w-72 h-44 mx-72 ">
									<p class="page text-sm absolute text-white">{{cardValue}}</p>
								</div>
							</div>
						</div>

						<div>
							<teleport to="#modal">
								<div v-if="isShowing">
									<div class="md:flex hidden">
										<div class="program block mx-auto" >
											<img src="../assets/icon-complete.svg" class="tent absolute w-16">
											<span class="mt-10 text-center text-3xl block">THANK YOU!</span>
											<p class="mt-5 block text-center">We've added your card details</p>
											<button class="block mx-auto mt-10 border-2 bg-indigo-900 px-28 py-2 rounded text-white">Continue</button>
										</div>
									</div>
								</div>
							</teleport>


							<form @submit.prevent="showForm" v-if="!isShowing">
								<div>
									<label class="  absolute -mt-9 text-sm mx-52 ">CARDHOLDER NAME</label>
									<input type="text" placeholder=" e.g. Jane Appleseed" class="block mx-52 mt-52 border-2 rounded border-slate-300 w-8/12 py-1"  v-model="cardName">
								</div>
								<div>
									<label class="  absolute -mt-6 text-sm mx-52 ">CARD NAME</label>
									<input type="number" placeholder=" e.g. 1234 5678 9123 0000" class="block mx-52 mt-12 border-2 rounded border-slate-300 w-8/12 py-1"  v-model="cardNumber">
								</div>
								<div class="grid grid-cols-3">
									<div>
										<label class="absolute text-sm mx-52 mt-8">EXP.DATE</label>
										<input type="number"
										placeholder="MM" class="mx-52 mt-14 border-2 w-12" v-model="date">
									</div>
									<div>
										<label class="absolute text-sm mx-36 mt-8">(MM/YY)</label>
										<input type="number" class="mx-36 mt-14 border-2 w-12"
										placeholder="YY" 
										 v-model="month">
									</div>
									<div>
										<label class="absolute text-sm mx-24 mt-8">CVC</label>
										<input type="number" class="mx-24 mt-14 border-2 w-20"
										placeholder="000"
										v-model="cardValue">
									</div>
								</div>
								<div>
									<button class="pin bg-indigo-900 block mt-5 py-2 text-white px-32  rounded font-bold text-lg w-[344px] text-sm">Continue</button>
								</div>
							</form>
						</div>
					</div>
				</div>
			</div>
	</div>
</template>


<script setup>
import {ref} from 'vue'
import Modal from '../components/Modal.vue'

const isShowing = ref(false)
const cardName = ref("Janet Appleseed")
const cardNumber = ref("0000 0000 0000 0000")
const date = ref("00/00")
const year = ref("")
const cardValue = ref("000")
const errors = ref("")
const hide = ref(true)


const showForm = () => {
	let	getAllValues = {
	cardName: cardName.value,
	cardNumber: cardNumber.value,
	date: date.value,
	year: year.value,
	cardValue: cardValue.value
}

	if(getAllValues){
		console.log('Form submitted!!!')
		isShowing.value = !isShowing.value
		errors.value = "Card Details Complete";
	}else if(!getAllValues){
		errors.value = "Card Details Incomplete"
		console.log("errors>>", errors.value)
	}

	if(cardName.value === ""){
		errors.value = "Please input card name"
	}
	if(cardValue.value === ""){
		errors.value = "Please input card value "
	}
	if(date.value === ""){
		errors.value = "Please insert a date"
	}
	if(year.value === ""){
		errors.value = "Please insert a year"
	}
	if(!cardNumber.value){
		errors.value = " Please insert card Number"
	}
	console.log('errors', errors.value)
}

</script>

<style scoped>
.pad {
	margin-left: 297px;
	font-size: 12px;
	margin-top: -79px;
}
.field{
	font-size:11px;
	margin-left: 30px;
}
.fields{
	font-size:11px;
	margin-left: 260px;
}
.text{
	font-size:19px;	
}
.card{
	margin-left: -150px;
}
.cards{
	margin-left: -190px;
}
.font{
	font-size: 10px;
}
.fonts{
	font-size: 10px;
	margin-left: 426px;
}
.img{
	margin-top: 310px;
}
.page{
	margin-left: 510px;
	margin-top: -99px;
}
.pin{
	margin-left: 205px;
}
.tent{
	margin-left: 120px;
	margin-top: -40px;
}
.program{
	margin-top: -490px;
	margin-left: 650px;
}
</style>
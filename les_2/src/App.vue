<script>
import Header from '@/components/Header.vue';
import Home from '@/components/Home.vue';

export default {
	components: { Header, Home },

	data() {
		return {
			nav: ["Home", "Marketplace", "Creators", "Resource"],
			cart_icon: "Connect Wallet"
		};
	},

}
</script>

<template>
	<Header />
	<Home />
</template>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;

	--white: #fff;
	--black: #000;
	--accent: #4aed52;
	--primary-1: #e40fac;
	--primary-2: #bd24e6;
	--accent-gradient: -gradient(#E40FAC, #BD24E6);

	--border-radius: 6px;

	--transition: .4s ease-in-out;
}

ul,
li {
	list-style: none;
}

body {
	font-family: 'Courier New', Courier, monospace;
	font-size: 20px;
	line-height: 24px;
}

.container {
	max-width: 1340px;
	padding: 0 90px;
	margin: 0 auto;
}
</style>

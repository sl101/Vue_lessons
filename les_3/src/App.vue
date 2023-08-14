<template>
	<div class="container mx-auto flex flex-col items-center bg-gray-100 p-4">
		<!--<div class="fixed w-100 h-100 opacity-80 bg-purple-800 inset-0 z-50 flex items-center justify-center">

<svg class="animate-spin -ml-1 mr-3 h-12 w-12 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
      <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
      <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
    </svg>

</div>-->
		<div class="container">
			<section>
				<form @submit.prevent="add">
					<div class="flex">
						<div class="max-w-xs">
							<label
								for="wallet"
								class="block text-s m font-medium text-gray-700"
								>Тикер</label
							>
							<div class="mt-1 relative rounded-md shadow-md">
								<input
									v-model="ticker"
									type="text"
									name="wallet"
									id="wallet"
									class="block w-full pr-10 border-gray-300 text-gray-900 focus:outline-none focus:ring-gray-500 focus:border-gray-500 sm:text-sm rounded-md"
									placeholder="Например DOGE"
								/>
							</div>

							<ul
								v-if="coins_show"
								class="flex bg-white shadow-md p-1 rounded-md shadow-md flex-wrap"
							>
								<li
									class="inline-flex items-center px-2 m-1 rounded-md text-xs font-medium bg-gray-300 text-gray-800 cursor-pointer"
									v-for="(coin, index) in filteredCoins.slice(0, 4)"
									:key="index"
									@click="inputTickers(coin.Symbol)"
								>
									{{ coin.Symbol }}
								</li>
							</ul>
							<div v-if="ticker_exists" class="text-sm text-red-600">
								Такой тикер уже добавлен
							</div>
						</div>
					</div>
					<button
						type="submit"
						class="my-4 inline-flex items-center py-2 px-4 border border-transparent shadow-sm text-sm leading-4 font-medium rounded-full text-white bg-gray-600 hover:bg-gray-700 transition-colors duration-300 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-gray-500"
					>
						<svg
							class="-ml-0.5 mr-2 h-6 w-6"
							xmlns="http://www.w3.org/2000/svg"
							width="30"
							height="30"
							viewBox="0 0 24 24"
							fill="#ffffff"
						>
							<path
								d="M13 7h-2v4H7v2h4v4h2v-4h4v-2h-4V7zm-1-5C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm0 18c-4.41 0-8-3.59-8-8s3.59-8 8-8 8 3.59 8 8-3.59 8-8 8z"
							></path>
						</svg>
						Добавить
					</button>
				</form>
			</section>

			<template v-if="tickers.length">
				<hr class="w-full border-t border-gray-600 my-4" />
				<dl class="mt-5 grid grid-cols-1 gap-5 sm:grid-cols-3">
					<div
						v-for="(t_item, index) in tickers"
						:key="index"
						@click.stop="graph_title = t_item"
						:class="{
							'border-4': graph_title === t_item,
						}"
						class="bg-white overflow-hidden shadow rounded-lg border-purple-800 border-solid cursor-pointer"
					>
						<div class="px-4 py-5 sm:p-6 text-center">
							<dt class="text-sm font-medium text-gray-500 truncate">
								{{ t_item.Symbol }} - USD
							</dt>
							<dd
								v-if="t_item.value"
								class="mt-1 text-3xl font-semibold text-gray-900"
							>
								{{ t_item.value }}
							</dd>
							<dd v-else class="mt-1 text-3xl font-regular text-gray-500">
								loading ...
							</dd>
						</div>
						<div class="w-full border-t border-gray-200"></div>
						<button
							@click.stop="remove(t_item.Symbol)"
							class="flex items-center justify-center font-medium w-full bg-gray-100 px-4 py-4 sm:px-6 text-md text-gray-500 hover:text-gray-600 hover:bg-gray-200 hover:opacity-20 transition-all focus:outline-none"
						>
							<svg
								class="h-5 w-5"
								xmlns="http://www.w3.org/2000/svg"
								viewBox="0 0 20 20"
								fill="#718096"
								aria-hidden="true"
							>
								<path
									fill-rule="evenodd"
									d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z"
									clip-rule="evenodd"
								></path></svg
							>Удалить
						</button>
					</div>
				</dl>

				<!--<div
          class="bg-white overflow-hidden shadow rounded-lg border-purple-800 border-solid cursor-pointer"
        >
          <div class="px-4 py-5 sm:p-6 text-center">
            <dt class="text-sm font-medium text-gray-500 truncate">
              WTF - USD
            </dt>
            <dd class="mt-1 text-3xl font-semibold text-gray-900">
              1.11
            </dd>
          </div>
          <div class="w-full border-t border-gray-200"></div>
          <button
            class="flex items-center justify-center font-medium w-full bg-gray-100 px-4 py-4 sm:px-6 text-md text-gray-500 hover:text-gray-600 hover:bg-gray-200 hover:opacity-20 transition-all focus:outline-none"
          >
            <svg
              class="h-5 w-5"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 20 20"
              fill="#718096"
              aria-hidden="true"
            >
              <path
                fill-rule="evenodd"
                d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z"
                clip-rule="evenodd"
              ></path></svg>Удалить
          </button>
        </div>
        <div
          class="bg-white overflow-hidden shadow rounded-lg border-purple-800 border-solid border-4 cursor-pointer"
        >
          <div class="px-4 py-5 sm:p-6 text-center">
            <dt class="text-sm font-medium text-gray-500 truncate">
              VUE - RUB
            </dt>
            <dd class="mt-1 text-3xl font-semibold text-gray-900">
              80000.00
            </dd>
          </div>
          <div class="w-full border-t border-gray-200"></div>
          <button
            class="flex items-center justify-center font-medium w-full bg-gray-100 px-4 py-4 sm:px-6 text-md text-gray-500 hover:text-gray-600 hover:bg-gray-200 hover:opacity-20 transition-all focus:outline-none"
          >
            <svg
              class="h-5 w-5"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 20 20"
              fill="#718096"
              aria-hidden="true"
            >
              <path
                fill-rule="evenodd"
                d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z"
                clip-rule="evenodd"
              ></path></svg>Удалить
          </button>
        </div>
        <div
          class="bg-white overflow-hidden shadow rounded-lg border-purple-800 border-solid cursor-pointer"
        >
          <div class="px-4 py-5 sm:p-6 text-center">
            <dt class="text-sm font-medium text-gray-500 truncate">
              BTC - USD
            </dt>
            <dd class="mt-1 text-3xl font-semibold text-gray-900">
              99999.99
            </dd>
          </div>
          <div class="w-full border-t border-gray-200"></div>
          <button
            class="flex items-center justify-center font-medium w-full bg-gray-100 px-4 py-4 sm:px-6 text-md text-gray-500 hover:text-gray-600 hover:bg-gray-200 hover:opacity-20 transition-all focus:outline-none"
          >
            <svg
              class="h-5 w-5"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 20 20"
              fill="#718096"
              aria-hidden="true"
            >
              <path
                fill-rule="evenodd"
                d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z"
                clip-rule="evenodd"
              ></path></svg>Удалить
          </button>
        </div>
        <div
          class="bg-white overflow-hidden shadow rounded-lg border-purple-800 border-solid cursor-pointer"
        >
          <div class="px-4 py-5 sm:p-6 text-center">
            <dt class="text-sm font-medium text-gray-500 truncate">
              DOGE - USD
            </dt>
            <dd class="mt-1 text-3xl font-semibold text-gray-900">
              0.0014
            </dd>
          </div>
          <div class="w-full border-t border-gray-200"></div>
          <button
            class="flex items-center justify-center font-medium w-full bg-gray-100 px-4 py-4 sm:px-6 text-md text-gray-500 hover:text-gray-600 hover:bg-gray-200 hover:opacity-20 transition-all focus:outline-none"
          >
            <svg
              class="h-5 w-5"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 20 20"
              fill="#718096"
              aria-hidden="true"
            >
              <path
                fill-rule="evenodd"
                d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z"
                clip-rule="evenodd"
              ></path></svg>Удалить
          </button>
        </div>-->
				<hr class="w-full border-t border-gray-600 my-4" />
			</template>
			<section v-if="graph_title" class="relative">
				<h3 class="text-lg leading-6 font-medium text-gray-900 my-8">
					{{ graph_title.Symbol }} - USD
				</h3>
				<div class="flex items-end border-gray-600 border-b border-l h-64">
					<div class="bg-purple-800 border w-10 h-24"></div>
					<div class="bg-purple-800 border w-10 h-32"></div>
					<div class="bg-purple-800 border w-10 h-48"></div>
					<div class="bg-purple-800 border w-10 h-16"></div>
				</div>
				<button
					@click="graph_title = null"
					type="button"
					class="absolute top-0 right-0"
				>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						xmlns:xlink="http://www.w3.org/1999/xlink"
						xmlns:svgjs="http://svgjs.com/svgjs"
						version="1.1"
						width="30"
						height="30"
						x="0"
						y="0"
						viewBox="0 0 511.76 511.76"
						style="enable-background: new 0 0 512 512"
						xml:space="preserve"
					>
						<g>
							<path
								d="M436.896,74.869c-99.84-99.819-262.208-99.819-362.048,0c-99.797,99.819-99.797,262.229,0,362.048    c49.92,49.899,115.477,74.837,181.035,74.837s131.093-24.939,181.013-74.837C536.715,337.099,536.715,174.688,436.896,74.869z     M361.461,331.317c8.341,8.341,8.341,21.824,0,30.165c-4.16,4.16-9.621,6.251-15.083,6.251c-5.461,0-10.923-2.091-15.083-6.251    l-75.413-75.435l-75.392,75.413c-4.181,4.16-9.643,6.251-15.083,6.251c-5.461,0-10.923-2.091-15.083-6.251    c-8.341-8.341-8.341-21.845,0-30.165l75.392-75.413l-75.413-75.413c-8.341-8.341-8.341-21.845,0-30.165    c8.32-8.341,21.824-8.341,30.165,0l75.413,75.413l75.413-75.413c8.341-8.341,21.824-8.341,30.165,0    c8.341,8.32,8.341,21.824,0,30.165l-75.413,75.413L361.461,331.317z"
								fill="#718096"
								data-original="#000000"
							></path>
						</g>
					</svg>
				</button>
			</section>
		</div>
	</div>
</template>

<script>
import axios from "axios";
import { api_key } from "./env.local";
export default {
	name: "App",
	data() {
		return {
			ticker: "",
			tickers: [],
			graph_title: null,
			graph: [],
			coins: [],
			coins_names: [],
			coins_show: false,
			ticker_exists: false,
		};
	},
	methods: {
		add() {
			if (this.ticker) {
				if (!this.checkTickers(this.ticker)) {
					const newTicker = {
						Symbol: this.ticker,
						value: "",
					};

					this.tickers.push(newTicker);
					this.fetchGraphData(newTicker);
					this.coins_show = false;
					this.ticker = "";
				}
			}
		},
		remove(name) {
			this.tickers = this.tickers.filter((elem) => elem.Symbol !== name);
			if (this.graph_title?.Symbol === name) {
				this.graph_title = null;
			}
		},

		checkTickers(title) {
			const tickers_names = this.tickers.map((item) => item.Symbol);

			if (tickers_names.some((elem) => elem === title)) {
				this.ticker_exists = true;
				return true;
			} else {
				this.ticker_exists = false;
				return false;
			}
		},

		inputTickers(symbol) {
			this.ticker = symbol;
		},

		fetchGraphData(newTicker) {
			setInterval(async () => {
				try {
					const response = await axios(
						`https://min-api.cryptocompare.com/data/price?fsym=${newTicker.Symbol}&tsyms=USD&api_key=5fe26ca8e9e8c0b1924366055147015e23c2e8ccf981f43c5dcd35bf81baa252`
					);
					const value =
						response.data.USD > 1
							? response.data.USD.toFixed(2)
							: response.data.USD.toPrecision(2);

					this.tickers.find((item) => item.Symbol === newTicker.Symbol).value =
						value;
				} catch (error) {
					console.log(error);
				}
			}, 5000);
		},

		async fetchCoinsList() {
			try {
				const response = await axios(
					`https://min-api.cryptocompare.com/data/all/coinlist?summary=true`
				);
				this.coins = Object.values(response.data.Data);
				this.coins_names = this.coins.map((coin) => coin.Symbol);
			} catch (error) {
				console.log(error);
			}
		},
	},
	computed: {
		filteredCoins() {
			if (this.ticker === "") {
				this.coins_show = false;
				return [];
			} else {
				this.coins_show = true;
				const searchTermLower = this.ticker.toLowerCase();

				return this.coins.filter((coin) => {
					return (
						coin.Symbol.toLowerCase().includes(searchTermLower) ||
						coin.FullName.toLowerCase().includes(searchTermLower)
					);
				});
			}
		},
	},
	mounted() {
		this.fetchCoinsList();
	},
};
</script>

<style></style>

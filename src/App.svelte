<script>
// import { requestAccountAddress, waitForAccountAuth } from "@celo/dappkit";

import { ethers } from 'ethers';

import { web3, connected, chainId, chainData, defaultEvmStores, selectedAccount } from 'svelte-web3';
// import { defaultEvmStores, connected, chainId, chainData, provider, signer, signerAddress } from 'svelte-ethers-store';

// import { newKit } from '@celo/contractkit';

// import { newKitFromWeb3 } from "@celo/contractkit";


import { CeloProvider } from '@celo-tools/celo-ethers-wrapper';
import { CeloWallet } from "@celo-tools/celo-ethers-wrapper";

// const provider = new CeloProvider("https://alfajores-forno.celo-testnet.org");
// await provider.ready;

// const wallet = new CeloWallet(YOUR_PK, provider);

const Web3Modal = window.Web3Modal.default;
const WalletConnectProvider = window.WalletConnectProvider.default;


// console.log(window);


let contract_abi = [{"type":"constructor","stateMutability":"nonpayable","payable":false,"inputs":[{"type":"bool","name":"test","internalType":"bool"}]},{"type":"event","name":"Approval","inputs":[{"type":"address","name":"owner","internalType":"address","indexed":true},{"type":"address","name":"spender","internalType":"address","indexed":true},{"type":"uint256","name":"value","internalType":"uint256","indexed":false}],"anonymous":false},{"type":"event","name":"OwnershipTransferred","inputs":[{"type":"address","name":"previousOwner","internalType":"address","indexed":true},{"type":"address","name":"newOwner","internalType":"address","indexed":true}],"anonymous":false},{"type":"event","name":"RegistrySet","inputs":[{"type":"address","name":"registryAddress","internalType":"address","indexed":true}],"anonymous":false},{"type":"event","name":"Transfer","inputs":[{"type":"address","name":"from","internalType":"address","indexed":true},{"type":"address","name":"to","internalType":"address","indexed":true},{"type":"uint256","name":"value","internalType":"uint256","indexed":false}],"anonymous":false},{"type":"event","name":"TransferComment","inputs":[{"type":"string","name":"comment","internalType":"string","indexed":false}],"anonymous":false},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"uint256","name":"","internalType":"uint256"}],"name":"allowance","inputs":[{"type":"address","name":"owner","internalType":"address"},{"type":"address","name":"spender","internalType":"address"}],"constant":true},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"approve","inputs":[{"type":"address","name":"spender","internalType":"address"},{"type":"uint256","name":"value","internalType":"uint256"}],"constant":false},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"uint256","name":"","internalType":"uint256"}],"name":"balanceOf","inputs":[{"type":"address","name":"owner","internalType":"address"}],"constant":true},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"uint8","name":"","internalType":"uint8"}],"name":"decimals","inputs":[],"constant":true},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"decreaseAllowance","inputs":[{"type":"address","name":"spender","internalType":"address"},{"type":"uint256","name":"value","internalType":"uint256"}],"constant":false},{"type":"function","stateMutability":"pure","payable":false,"outputs":[{"type":"uint256","name":"","internalType":"uint256"},{"type":"uint256","name":"","internalType":"uint256"},{"type":"uint256","name":"","internalType":"uint256"},{"type":"uint256","name":"","internalType":"uint256"}],"name":"getVersionNumber","inputs":[],"constant":true},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"increaseAllowance","inputs":[{"type":"address","name":"spender","internalType":"address"},{"type":"uint256","name":"value","internalType":"uint256"}],"constant":false},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[],"name":"increaseSupply","inputs":[{"type":"uint256","name":"amount","internalType":"uint256"}],"constant":false},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[],"name":"initialize","inputs":[{"type":"address","name":"registryAddress","internalType":"address"}],"constant":false},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"initialized","inputs":[],"constant":true},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"isOwner","inputs":[],"constant":true},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"mint","inputs":[{"type":"address","name":"to","internalType":"address"},{"type":"uint256","name":"value","internalType":"uint256"}],"constant":false},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"string","name":"","internalType":"string"}],"name":"name","inputs":[],"constant":true},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"address","name":"","internalType":"address"}],"name":"owner","inputs":[],"constant":true},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"address","name":"","internalType":"contract IRegistry"}],"name":"registry","inputs":[],"constant":true},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[],"name":"renounceOwnership","inputs":[],"constant":false},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[],"name":"setRegistry","inputs":[{"type":"address","name":"registryAddress","internalType":"address"}],"constant":false},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"string","name":"","internalType":"string"}],"name":"symbol","inputs":[],"constant":true},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"uint256","name":"","internalType":"uint256"}],"name":"totalSupply","inputs":[],"constant":true},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"transfer","inputs":[{"type":"address","name":"to","internalType":"address"},{"type":"uint256","name":"value","internalType":"uint256"}],"constant":false},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"transferFrom","inputs":[{"type":"address","name":"from","internalType":"address"},{"type":"address","name":"to","internalType":"address"},{"type":"uint256","name":"value","internalType":"uint256"}],"constant":false},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[],"name":"transferOwnership","inputs":[{"type":"address","name":"newOwner","internalType":"address"}],"constant":false},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"transferWithComment","inputs":[{"type":"address","name":"to","internalType":"address"},{"type":"uint256","name":"value","internalType":"uint256"},{"type":"string","name":"comment","internalType":"string"}],"constant":false}];

let contract_address = '0x471EcE3750Da237f93B8E339c536989b8978a438';
// let contract_address = '0xF469829b3b0D7f696720B34BDE0284E628bD448e';



async function enable_1() {

	// let web3Modal = new Web3Modal({
	// 	// cacheProvider: false,
	// 	providerOptions: {
	// 	// 	"custom-example": {
	// 	// 	display: {
	// 	// 	logo: "data:image/gif;base64,INSERT_BASE64_STRING",
	// 	// 	name: "Example Provider",
	// 	// 	description: "Connect to your example provider account"
	// 	// 	},
	// 	// 	package: ExampleProvider,
	// 	// 	options: {
	// 	// 	apiKey: "EXAMPLE_PROVIDER_API_KEY"
	// 	// 	},
	// 	// 	connector: async (ProviderPackage, options) => {
	// 	// 	const provider = new ProviderPackage(options);

	// 	// 	await provider.enable();

	// 	// 	return provider;
	// 	// 	}
	// 	// 	}


	// 		walletconnect: {
	// 			package: WalletConnectProvider,
	// 			// package: CeloProvider,
	// 			// package: null,
	// 			options: {
	// 				// infuraId: "infura_id",
	// 				rpc: {
	// 					// 44787: "https://alfajores-forno.celo-testnet.org",
	// 					42220: "https://forno.celo.org",
	// 				},
	// 				// qrcode: false,
	// 				qrcodeModalOptions: {
	// 					desktopLinks: [
	// 						// "MetaMask",
	// 					],
	// 					mobileLinks: [
	// 						"Valora",
	// 						"Celo Wallet"
	// 					],
	// 				},
	// 			},
	// 		},

	// 	},
	// 	disableInjectedProvider: false,
	// 	// disableInjectedsetBrowserProvider: false,
	// 	disableInjectedsetBrowserProvider: false,
	// });

	// // alert('1.');

	// const provider = await web3Modal.connect();

	
	const provider = new WalletConnectProvider({
		rpc: {
			// 44787: "https://alfajores-forno.celo-testnet.org",
			42220: "https://forno.celo.org",
		},
		qrcodeModalOptions: {
			desktopLinks: [
				// "MetaMask",
			],
			mobileLinks: [
				"Valora",
				"Celo Wallet"
			],
		},
	});

	await provider.enable();
	defaultEvmStores.setProvider(provider);


	// alert('Popup 1');




	// $web3.eth.accounts.signTransaction(tx, privateKey).then(signed => {
	// 	$web3.eth.sendSignedTransaction(signed.rawTransaction).on('receipt', console.log)
	// });



	// alert('Popup 2');


	// await contract_instance.methods.transfer(
	// 	'0x0AD0a97C7788D8762CB7B776750C103A064a4c60',
	// 	$web3.utils.toHex($web3.utils.toWei('0.01', "ether")),
	// )


	// alert('Popup 3');



	// const web3 = new Web3(provider);





	// await provider.ready;

	// console.log(provider);

	// const prov = new ethers.providers.Web3Provider(provider);

	// console.log(prov);


}


async function enable_2() {

	let web3Modal = new Web3Modal({
		// cacheProvider: false,
		providerOptions: {
		// 	"custom-example": {
		// 	display: {
		// 	logo: "data:image/gif;base64,INSERT_BASE64_STRING",
		// 	name: "Example Provider",
		// 	description: "Connect to your example provider account"
		// 	},
		// 	package: ExampleProvider,
		// 	options: {
		// 	apiKey: "EXAMPLE_PROVIDER_API_KEY"
		// 	},
		// 	connector: async (ProviderPackage, options) => {
		// 	const provider = new ProviderPackage(options);

		// 	await provider.enable();

		// 	return provider;
		// 	}
		// 	}


			walletconnect: {
				package: WalletConnectProvider,
				// package: CeloProvider,
				// package: null,
				options: {
					// infuraId: "infura_id",
					rpc: {
						// 44787: "https://alfajores-forno.celo-testnet.org",
						42220: "https://forno.celo.org",
					},
					// qrcode: false,
					qrcodeModalOptions: {
						desktopLinks: [
							// "MetaMask",
						],
						mobileLinks: [
							"Valora",
							"Celo Wallet"
						],
					},
				},
			},

		},
		disableInjectedProvider: false,
		// disableInjectedsetBrowserProvider: false,
		disableInjectedsetBrowserProvider: false,
	});

	// alert('1.');

	const provider = await web3Modal.connect();


	defaultEvmStores.setProvider(provider);


}



async function enable() {

	// alert('0.');

	let web3Modal = new Web3Modal({
		// cacheProvider: false,
		providerOptions: {
		// 	"custom-example": {
		// 	display: {
		// 	logo: "data:image/gif;base64,INSERT_BASE64_STRING",
		// 	name: "Example Provider",
		// 	description: "Connect to your example provider account"
		// 	},
		// 	package: ExampleProvider,
		// 	options: {
		// 	apiKey: "EXAMPLE_PROVIDER_API_KEY"
		// 	},
		// 	connector: async (ProviderPackage, options) => {
		// 	const provider = new ProviderPackage(options);

		// 	await provider.enable();

		// 	return provider;
		// 	}
		// 	}


			walletconnect: {
				package: WalletConnectProvider,
				// package: CeloProvider,
				// package: null,
				options: {
					// infuraId: "infura_id",
					rpc: {
						// 44787: "https://alfajores-forno.celo-testnet.org",
						42220: "https://forno.celo.org",
					},
					// qrcode: false,
					qrcodeModalOptions: {
						desktopLinks: [
							// "MetaMask",
						],
						mobileLinks: [
							"Valora",
							"Celo Wallet"
						],
					},
				},
			},

		},
		disableInjectedProvider: false,
		// disableInjectedsetBrowserProvider: false,
		disableInjectedsetBrowserProvider: false,
	});

	// alert('1.');

	const instance = await web3Modal.connect();

	const prov = new ethers.providers.Web3Provider(instance);

	// const provider = new CeloProvider(instance);
	// const provider = await web3Modal.connect();
	defaultEvmStores.setProvider(prov);

	// console.log(provider);

	// console.log(defaultEvmStores.getDefaultProvider());

}



// let contract_abi = [{"type":"constructor","stateMutability":"nonpayable","payable":false,"inputs":[{"type":"bool","name":"test","internalType":"bool"}]},{"type":"event","name":"Approval","inputs":[{"type":"address","name":"owner","internalType":"address","indexed":true},{"type":"address","name":"spender","internalType":"address","indexed":true},{"type":"uint256","name":"value","internalType":"uint256","indexed":false}],"anonymous":false},{"type":"event","name":"OwnershipTransferred","inputs":[{"type":"address","name":"previousOwner","internalType":"address","indexed":true},{"type":"address","name":"newOwner","internalType":"address","indexed":true}],"anonymous":false},{"type":"event","name":"RegistrySet","inputs":[{"type":"address","name":"registryAddress","internalType":"address","indexed":true}],"anonymous":false},{"type":"event","name":"Transfer","inputs":[{"type":"address","name":"from","internalType":"address","indexed":true},{"type":"address","name":"to","internalType":"address","indexed":true},{"type":"uint256","name":"value","internalType":"uint256","indexed":false}],"anonymous":false},{"type":"event","name":"TransferComment","inputs":[{"type":"string","name":"comment","internalType":"string","indexed":false}],"anonymous":false},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"uint256","name":"","internalType":"uint256"}],"name":"allowance","inputs":[{"type":"address","name":"owner","internalType":"address"},{"type":"address","name":"spender","internalType":"address"}],"constant":true},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"approve","inputs":[{"type":"address","name":"spender","internalType":"address"},{"type":"uint256","name":"value","internalType":"uint256"}],"constant":false},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"uint256","name":"","internalType":"uint256"}],"name":"balanceOf","inputs":[{"type":"address","name":"owner","internalType":"address"}],"constant":true},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"uint8","name":"","internalType":"uint8"}],"name":"decimals","inputs":[],"constant":true},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"decreaseAllowance","inputs":[{"type":"address","name":"spender","internalType":"address"},{"type":"uint256","name":"value","internalType":"uint256"}],"constant":false},{"type":"function","stateMutability":"pure","payable":false,"outputs":[{"type":"uint256","name":"","internalType":"uint256"},{"type":"uint256","name":"","internalType":"uint256"},{"type":"uint256","name":"","internalType":"uint256"},{"type":"uint256","name":"","internalType":"uint256"}],"name":"getVersionNumber","inputs":[],"constant":true},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"increaseAllowance","inputs":[{"type":"address","name":"spender","internalType":"address"},{"type":"uint256","name":"value","internalType":"uint256"}],"constant":false},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[],"name":"increaseSupply","inputs":[{"type":"uint256","name":"amount","internalType":"uint256"}],"constant":false},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[],"name":"initialize","inputs":[{"type":"address","name":"registryAddress","internalType":"address"}],"constant":false},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"initialized","inputs":[],"constant":true},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"isOwner","inputs":[],"constant":true},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"mint","inputs":[{"type":"address","name":"to","internalType":"address"},{"type":"uint256","name":"value","internalType":"uint256"}],"constant":false},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"string","name":"","internalType":"string"}],"name":"name","inputs":[],"constant":true},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"address","name":"","internalType":"address"}],"name":"owner","inputs":[],"constant":true},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"address","name":"","internalType":"contract IRegistry"}],"name":"registry","inputs":[],"constant":true},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[],"name":"renounceOwnership","inputs":[],"constant":false},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[],"name":"setRegistry","inputs":[{"type":"address","name":"registryAddress","internalType":"address"}],"constant":false},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"string","name":"","internalType":"string"}],"name":"symbol","inputs":[],"constant":true},{"type":"function","stateMutability":"view","payable":false,"outputs":[{"type":"uint256","name":"","internalType":"uint256"}],"name":"totalSupply","inputs":[],"constant":true},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"transfer","inputs":[{"type":"address","name":"to","internalType":"address"},{"type":"uint256","name":"value","internalType":"uint256"}],"constant":false},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"transferFrom","inputs":[{"type":"address","name":"from","internalType":"address"},{"type":"address","name":"to","internalType":"address"},{"type":"uint256","name":"value","internalType":"uint256"}],"constant":false},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[],"name":"transferOwnership","inputs":[{"type":"address","name":"newOwner","internalType":"address"}],"constant":false},{"type":"function","stateMutability":"nonpayable","payable":false,"outputs":[{"type":"bool","name":"","internalType":"bool"}],"name":"transferWithComment","inputs":[{"type":"address","name":"to","internalType":"address"},{"type":"uint256","name":"value","internalType":"uint256"},{"type":"string","name":"comment","internalType":"string"}],"constant":false}];

// // let contract_address = '0x4DdeB8F7041aB3260c6ec5Afb6FEab0650F4ABB4';
// let contract_address = '0xF469829b3b0D7f696720B34BDE0284E628bD448e';


async function send() {

	let contract_bytecode = '0x6020610d5b6080396080518060801d81607f1d18610d565760e05260206020610d5b01608039608051610d5b01608060208260803960805111610d5657806020816080396080516020018082610100395050506702c68af0bb1400003410156100fe5760266101a0527f4e6f7420656e6f7567682043454c4f2073656e7420746f207468697320636f6e6101c0527f74726163742100000000000000000000000000000000000000000000000000006101e0526101a0506101a051806101c001818260206001820306601f82010390500336823750506308c379a0610160526020610180526101a05160206001820306601f820103905060440161017cfd5b600a60e05113156101805760146101a0527f546f6f206d616e7920726563697069656e7473210000000000000000000000006101c0526101a0506101a051806101c001818260206001820306601f82010390500336823750506308c379a0610160526020610180526101a05160206001820306601f820103905060440161017cfd5b3360005560e051600155610100806003602082510160c060006005818352015b8260c05160200211156101b2576101d1565b60c05160200285015160c05185015581516001018083528114156101a0575b505050505050610d3e56600436101561000d57610b57565b60046000601c3760005134610b5d576359b94b0081186105ec576004358060a01c610b5d5760e05273c7c1f793e9441e0abb593f0540a98c36d0b7eb6e33146100c4576013610100527f596f752063616e6e6f7420646f207468617421000000000000000000000000006101205261010050610100518061012001818260206001820306601f82010390500336823750506308c379a060c052602060e0526101005160206001820306601f820103905060440160dcfd5b60095415610140576012610100527f436f6d706c6574656420616c72656164792100000000000000000000000000006101205261010050610100518061012001818260206001820306601f82010390500336823750506308c379a060c052602060e0526101005160206001820306601f820103905060440160dcfd5b600a54156101bc576009610100527f46696e69736865642100000000000000000000000000000000000000000000006101205261010050610100518061012001818260206001820306601f82010390500336823750506308c379a060c052602060e0526101005160206001820306601f820103905060440160dcfd5b600254600154141561023c576012610100527f416c726561647920636f6d706c657465642100000000000000000000000000006101205261010050610100518061012001818260206001820306601f82010390500336823750506308c379a060c052602060e0526101005160206001820306601f820103905060440160dcfd5b3360005414156102ba576014610100527f4e6f7420796f7572206f776e207061636b6574210000000000000000000000006101205261010050610100518061012001818260206001820306601f82010390500336823750506308c379a060c052602060e0526101005160206001820306601f820103905060440160dcfd5b47610100526001546101205260025461014052610100516003808204905090506002808202821582848304141715610b5d57905090506024356002808202821582848304141715610b5d5790509050808210610b5d578082039050905061016052600161014051610120518082038060801d81607f1d18610b5d57905090501861037357610100516024356002808202821582848304141715610b5d5790509050808210610b5d57808203905090506101605260016009555b600060046101c0527fa9059cbb000000000000000000000000000000000000000000000000000000006101e0526101c06004806020846102000101826020850160045afa50508051820191505060e051602082610200010152602081019050610160516020826102000101526020810190508061020052610200505060206102a061020051610220600073471ece3750da237f93b8e339c536989b8978a4385af1610423573d600060003e3d6000fd5b61028060203d8082116104365781610438565b805b905090508152805160200180610180828460045afa9050505060006101805114610477576101a0516101805181816020036008021c9050905015610b5d575b60006004610200527fa9059cbb00000000000000000000000000000000000000000000000000000000610220526102006004806020846102400101826020850160045afa50508051820191505073c7c1f793e9441e0abb593f0540a98c36d0b7eb6e6020826102400101526020810190506024356002808202821582848304141715610b5d57905090506020826102400101526020810190508061024052610240505060206102e061024051610260600073471ece3750da237f93b8e339c536989b8978a4385af161054e573d600060003e3d6000fd5b6102c060203d8082116105615781610563565b805b9050905081528051602001806101c0828460045afa9050505060006101c051146105a2576101e0516101c05181816020036008021c9050905015610b5d575b7f33e725b04a06c793e0231dd3c946880af0697c3a0e1b5be1168c35c0e80fe6cb61016051610200526024356102205260e051610240526060610200a16001610200526020610200f35b63a5bc7a8781186107f157600a541561066f57601160e0527f416c726561647920726566756e646564210000000000000000000000000000006101005260e05060e0518061010001818260206001820306601f82010390500336823750506308c379a060a052602060c05260e05160206001820306601f820103905060440160bcfd5b60005433146106e857601360e0527f4e6f74206372656174656420627920796f7521000000000000000000000000006101005260e05060e0518061010001818260206001820306601f82010390500336823750506308c379a060a052602060c05260e05160206001820306601f820103905060440160bcfd5b60006004610120527fa9059cbb00000000000000000000000000000000000000000000000000000000610140526101206004806020846101600101826020850160045afa505080518201915050336020826101600101526020810190504760208261016001015260208101905080610160526101605050602061020061016051610180600073471ece3750da237f93b8e339c536989b8978a4385af1610793573d600060003e3d6000fd5b6101e060203d8082116107a657816107a8565b805b90509050815280516020018060e0828460045afa90505050600060e051146107e4576101005160e05181816020036008021c9050905015610b5d575b6001610120526020610120f35b63c916c4908118610a0a57600a541561087457601160e0527f416c726561647920726566756e646564210000000000000000000000000000006101005260e05060e0518061010001818260206001820306601f82010390500336823750506308c379a060a052602060c05260e05160206001820306601f820103905060440160bcfd5b73c7c1f793e9441e0abb593f0540a98c36d0b7eb6e33146108ff57601360e0527f4e6f74206372656174656420627920796f7521000000000000000000000000006101005260e05060e0518061010001818260206001820306601f82010390500336823750506308c379a060a052602060c05260e05160206001820306601f820103905060440160bcfd5b60006004610120527fa9059cbb00000000000000000000000000000000000000000000000000000000610140526101206004806020846101600101826020850160045afa5050805182019150506000546020826101600101526020810190504760208261016001015260208101905080610160526101605050602061020061016051610180600073471ece3750da237f93b8e339c536989b8978a4385af16109ac573d600060003e3d6000fd5b6101e060203d8082116109bf57816109c1565b805b90509050815280516020018060e0828460045afa90505050600060e051146109fd576101005160e05181816020036008021c9050905015610b5d575b6001610120526020610120f35b6302d05d3f8118610a215760005460e052602060e0f35b638b40f4e98118610a385760015460e052602060e0f35b6363ee4e2b8118610a4f5760025460e052602060e0f35b63e21f37ce8118610af25760e08060208082528083018060038082602082540160c060006005818352015b8260c0516020021115610a8c57610aab565b60c05185015460c0516020028501528151600101808352811415610a7a575b5050505050508051806020830101818260206001820306601f8201039050033682375050805160200160206001820306601f820103905090509050810190509050905060e0f35b63eb8203128118610b27576004358060a01c610b5d5760e052600860e05160a052608052604060802054610100526020610100f35b639d9a7fe98118610b3e5760095460e052602060e0f35b63a104d7a28118610b5557600a5460e052602060e0f35b505b60006000fd5b600080fd5b6101dc610d3e036101dc6000396101dc610d3e036000f35b600080fd';


	let contract_abi = [{"name": "PacketReceived", "inputs": [{"name": "_value", "type": "uint256", "indexed": false}, {"name": "_gas_x_2", "type": "uint256", "indexed": false}, {"name": "_address", "type": "address", "indexed": false}], "anonymous": false, "type": "event"}, {"stateMutability": "payable", "type": "constructor", "inputs": [{"name": "_number_of_recipients_to_receive", "type": "int128"}, {"name": "_message", "type": "string"}], "outputs": []}, {"stateMutability": "nonpayable", "type": "function", "name": "receive_packet_drop", "inputs": [{"name": "_address", "type": "address"}, {"name": "_estimated_gas", "type": "uint256"}], "outputs": [{"name": "", "type": "bool"}], "gas": 85466}, {"stateMutability": "nonpayable", "type": "function", "name": "refund_packet", "inputs": [], "outputs": [{"name": "", "type": "bool"}], "gas": 18648}, {"stateMutability": "nonpayable", "type": "function", "name": "refund_packet_by_owner", "inputs": [], "outputs": [{"name": "", "type": "bool"}], "gas": 18679}, {"stateMutability": "view", "type": "function", "name": "creator", "inputs": [], "outputs": [{"name": "", "type": "address"}], "gas": 2550}, {"stateMutability": "view", "type": "function", "name": "number_of_recipients_to_receive", "inputs": [], "outputs": [{"name": "", "type": "int128"}], "gas": 2580}, {"stateMutability": "view", "type": "function", "name": "number_of_recipients_received", "inputs": [], "outputs": [{"name": "", "type": "int128"}], "gas": 2610}, {"stateMutability": "view", "type": "function", "name": "message", "inputs": [], "outputs": [{"name": "", "type": "string"}], "gas": 17471}, {"stateMutability": "view", "type": "function", "name": "recipients", "inputs": [{"name": "arg0", "type": "address"}], "outputs": [{"name": "", "type": "uint256"}], "gas": 2936}, {"stateMutability": "view", "type": "function", "name": "completed", "inputs": [], "outputs": [{"name": "", "type": "bool"}], "gas": 2700}, {"stateMutability": "view", "type": "function", "name": "refunded_to_creator", "inputs": [], "outputs": [{"name": "", "type": "bool"}], "gas": 2730}];


	let contract_instance = new $web3.eth.Contract(
		contract_abi,
	);


	let encoded = contract_instance.deploy({
		data: contract_bytecode,
		arguments: [
			3,
			'Hello',
		],
	}).encodeABI();


	// console.log($web3.eth);


	// let contract_instance = new $web3.eth.Contract(
	// 	contract_abi,
	// 	contract_address,
	// );


	// let encoded = contract_instance.methods.transfer(
	// 	'0x0AD0a97C7788D8762CB7B776750C103A064a4c60',
	// 	$web3.utils.toHex($web3.utils.toWei('0.002', "ether")),
	// ).encodeABI();


	// data: '0x61022c56600436101561000d57610221565b60046000601c3760005163baaadce481186100425734610223576000600060006000662386f26fc10000336000f11561022357005b6381c9a249811861010657346102235763fc4847266101005243610120526020610100602461011c7367c6829506ddf66ed824fd1ccc40665588bc46315afa610090573d600060003e3d6000fd5b601f3d1115610223576101005160e0526323b872dd6101005233610120523061014052600435610160526020610100606461011c6000736d0081857009cb79014df13e34fc49192f66aee15af16100ec573d600060003e3d6000fd5b601f3d111561022357610100506001610100526020610100f35b622b7804811861021f576024358060a01c6102235760e052346102235760006004610140527fa9059cbb00000000000000000000000000000000000000000000000000000000610160526101406004806020846101800101826020850160045afa50508051820191505033602082610180010152602081019050600435602082610180010152602081019050806101805261018050506020610220610180516101a0600060e0515af16101be573d600060003e3d6000fd5b61020060203d8082116101d157816101d3565b805b905090508152805160200180610100828460045afa905050506000610100511461021257610120516101005181816020036008021c9050905015610223575b6001610140526020610140f35b505b005b600080fd5b61000461022c0361000460003961000461022c036000f3',


	let tx = {
		data: encoded,
		// arguments: [
		// 	3,
		// 	'Hello',
		// ],
		from: $selectedAccount,
		value: $web3.utils.toHex($web3.utils.toWei('0.25', 'ether')),
		// gasLimit: $web3.utils.toHex('60000'),
	}


	alert('Ok Thanks');


	$web3.eth.sendTransaction(tx).then(data => {
		alert('1');
		alert(data);
	});


	// body...
	// console.log($signer);
	// console.log($provider);


	// const params = [{
 //		from: $signerAddress,
 //		to: '0xc7c1f793E9441e0abB593f0540a98c36d0b7Eb6E',
 //		value: ethers.utils.parseUnits('0.01', 'ether').toHexString(),
 //	}];

 //	const transactionHash = await $provider.send('eth_sendTransaction', params)
 //	console.log('transactionHash is ' + transactionHash);


	// let contract_instance = new ethers.Contract(
	// 	contract_address,
	// 	contract_abi,
	// 	$signer,
	// );

	// // console.log($selectedAccount);
	// // console.log(defaultEvmStores.selectedAccount);

	// console.log($signerAddress);

	// let t = await contract_instance.transfer(
	// 	'0xc7c1f793E9441e0abB593f0540a98c36d0b7Eb6E',
	// 	$web3.utils.toWei('0.01', "ether"),
	// );

	// console.log(t);

}


// onMount(async() => {
// 	enable();
// });

</script>


<style>

</style>

<main>
	<button on:click={enable_1}>
		Connect Wallet
	</button>
	<br>
	{#if $connected}
		connected!
		<button on:click={send}>
			Send
		</button>
	{:else}
		not yet connected!
	{/if}
	<br>
	addr: {$selectedAccount}
	<br>
	chain_id: {$chainId}
	<br>
	updated :)
	<!-- {$provider} -->
	<!-- {$signer} -->
	<!-- <br> -->
	<!-- {$chainData} -->
</main>




<template>
  <button
    class="rounded shadow-md bg-white px-4 py-2 mx-2 leading-8"
    @click="connectMetamask"
  >
    
    Connect Metamask
  </button>
</template>

<script>
import Web3 from 'web3';
export default {
  name: 'ConnectMetamask',
//   data() {
//       return {
//         chainId: undefined,
//       }
//   },
  methods: {
    async connectMetamask() {
        if (typeof window.ethereum !== 'undefined') {
            var chainId = parseInt(window.ethereum.chainId);
            window.web3 = new Web3(window.ethereum);
            window.ethereum.enable();
            window.web3.eth.getAccounts((error,result) => {
                if(error){ console.log(error)}
                else{
                    var address = result
                    window.web3.eth.getBlockNumber((error,result) => {
                        if(error){ console.log(error)}
                        else{
                            var blocknum = result
                            this.$store.dispatch('login', {address, blocknum, chainId})
                        }
                    })
                }
            })
        }
        else {
            console.error('MetaMask is not detected!');
        }
    },
  },
};
</script>
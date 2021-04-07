<template>
    <p></p>
</template>

<script>
import Web3 from 'web3'
const abi = require('../../../contract/build/SongForACity.json').abi
const address = '0x004a84209a0021b8ff182ffd8bb874c53f65e90e'

export default ({
    setup() {
    },
    async mounted(){
        const web3 = new Web3(Web3.currentProvider || "http://localhost:7545")
        Web3.givenProvider.enable()

        var myContract = new web3.eth.Contract(abi, address);
        const nametoken = await myContract.methods.name().call()
        console.log(nametoken)
        // let web3 = window.web3 
        // if (web3){
        //     web3 = new Web3(web3.currentProvider)
        //     window.ethereum.enable()
        // }
        // web3.eth.defaultAccount = web3.eth.accounts[0];
        // console.log(web3.eth.defaultAccount)
        
        // var initContract = web3.eth.contract(abi);
        // var contract = initContract.at(address);

        // contract.totalSupply().call().then(function(result){
        //     console.log('result : ', result);
        // });
    }
})
</script>

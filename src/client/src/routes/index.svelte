<script>
  import { ethers } from "ethers";

  let walletAddress = ''
  let balance = 0

  async function func(){
    // provider…ブロックチェーンからデータを読み込むための読み込み先のことです。providerがデータを渡してくれます。
    let provider = new ethers.providers.Web3Provider(window.ethereum)
    let walletAddresses = await provider.send("eth_requestAccounts", [])
    console.log(provider)
    walletAddress = walletAddresses[0]
    
    // signer…ブロックチェーンへの書き込み手段です。一般的にはメタマスクなどがSingerに値します
    const signer = provider.getSigner()
    console.log(signer)

    // avalanche get
    balance = await provider.getBalance(walletAddress)
    balance = ethers.utils.formatEther(balance)
  }

  let promise = func()
</script>


{#await promise}
  <p>loading...</p>
{:then resolved}
  <p>{balance}</p>
{/await}

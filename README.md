# Onboard

JavaScript library to easily onboard users to ethereum apps by enabling wallet selection, connection, wallet checks and real time state updates.

## Install

`npm install @authereum/bnc-onboard@starkware`

## Quick Start

```javascript
import Onboard from '@authereum/bnc-onboard'

const BLOCKNATIVE_KEY = 'blocknative-api-key'
const NETWORK_ID = 3

const onboard = Onboard({
  dappId: BLOCKNATIVE_KEY,
  networkId: NETWORK_ID,
  starkConfig: {
    exchangeAddress: '0x4a2ac1e2ba79d4b73d86b5dbd1a05a627964b33c',

    // for non-native integrations, use signature based stark key
    authMessage: () => 'Example auth message: 123',
  },
  subscriptions: {
    wallet: async wallet => {
      // returns starkware-enable web3 provider
      const { provider } = wallet.provider

      const layer = 'starkex',
      const application = 'starkexdemo',
      const index = '0'

      const starkKey = await provider.account(layer, application, index)
      console.log(starkKey)

      // see: https://github.com/authereum/starkware-monorepo/tree/starkex-3.0/packages/starkware-provider
      const txhash = await provider.transfer({from, to, asset, ...})
      console.log(txhash)
    }
  }
})

await onboard.walletSelect()
await onboard.walletCheck()
```

## Documentation

For detailed documentation head to [docs.blocknative.com](https://docs.blocknative.com/onboard)

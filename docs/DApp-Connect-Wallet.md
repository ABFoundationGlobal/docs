### ABWallet DApp Integration Documentation

This document provides a guide for developers to integrate decentralized applications (DApps) with ABWallet, a cryptocurrency wallet supporting EVM, Tron, and Solana blockchains. The wallet's namespace is `window.abwallet`. This guide covers environment detection, connecting to supported blockchains, signing, and chain selection operations.

**Key Points**:
- **Environment Detection**: Use the provided `isInABWalletApp()` function to check if the user is in the ABWallet environment.
- **EVM Connection**: Access via `window.abwallet.ethereum`, following MetaMask protocols.
- **Tron Connection**: Access via `window.abwallet.tron`, similar to TronLink.
- **Notes**: Handle user rejection cases and verify the correct network is selected.

---

## 1. Detecting ABWallet Environment

Before connecting, verify if the user is in the ABWallet environment using the following function:

```javascript
export function isInABWalletApp() {
    if (typeof window !== 'undefined' && typeof window.navigator !== 'undefined') {
        return /ABWallet/i.test(window.navigator.userAgent);
    }
    return false;
}
```

- **Purpose**: Checks if the browser's user agent contains "ABWallet" to confirm the ABWallet environment.
- **Usage**:
  ```javascript
  if (isInABWalletApp()) {
      console.log('User is in ABWallet environment');
  } else {
      console.log('Please install ABWallet');
  }
  ```
- **Note**: This method relies on the user agent string, which may vary. Consider additional checks (e.g., `window.abwallet` existence) for reliability.

## 2. Connecting to EVM Chains

ABWallet supports EVM-compatible chains (e.g., Ethereum, Binance Smart Chain) via `window.abwallet.ethereum`, which follows MetaMask’s standard protocol (EIP-1193).

### 2.1 Connection Steps
1. **Get EVM Provider**:
   ```javascript
   var provider = window.abwallet.ethereum;
   ```
2. **Request User Accounts**:
   ```javascript
   provider.request({ method: 'eth_requestAccounts' })
       .then((accounts) => {
           console.log('Connected accounts:', accounts);
       })
       .catch((error) => {
           if (error.code === 4001) {
               console.log('User rejected connection');
           } else {
               console.error('Connection error:', error);
           }
       });
   ```
3. **Get Current Chain ID**:
   ```javascript
   provider.request({ method: 'eth_chainId' })
       .then((chainId) => {
           console.log('Current chain ID:', chainId);
       });
   ```
4. **Switch Network (if needed)**:
   ```javascript
   provider.request({
       method: 'wallet_switchEthereumChain',
       params: [{ chainId: '0x1' }] // Example: Switch to Ethereum Mainnet
   });
   ```

### 2.2 Signing Operations
- **Sign Message**:
  ```javascript
  provider.request({
      method: 'personal_sign',
      params: ['Message content', accounts[0]]
  }).then((signature) => {
      console.log('Signature:', signature);
  });
  ```

### 2.3 Notes
- **Error Handling**: Handle user rejection (error code 4001) and other errors.
- **Reference**: MetaMask developer documentation ([https://docs.metamask.io/](https://docs.metamask.io/)) applies to `window.abwallet.ethereum`.
- **Network Compatibility**: Ensure the user selects the correct EVM network (e.g., Mainnet or Testnet).

## 3. Connecting to Tron

ABWallet supports the Tron blockchain via `window.abwallet.tron`, with an interface similar to TronLink’s TronWeb.

### 3.1 Connection Steps
1. **Get Tron Provider**:
   ```javascript
   var tronProvider = window.abwallet.tron;
   ```
2. **Request User Accounts**:
   ```javascript
   tronProvider.request({
       method: 'tron_requestAccounts',
       params: {
           websiteIcon: 'https://your-dapp.com/icon.png',
           websiteName: 'Your DApp'
       }
   }).then((accounts) => {
       console.log('Connected Tron accounts:', accounts);
   }).catch((error) => {
       if (error.code === 4001) {
           console.log('User rejected connection');
       } else {
           console.error('Connection error:', error);
       }
   });
   ```
3. **Get Default Address**:
   ```javascript
   if (tronProvider && tronProvider.defaultAddress.base58) {
       console.log('Default address:', tronProvider.defaultAddress.base58);
   }
   ```

### 3.2 Signing Operations
- **Sign Transaction**:
  ```javascript
  const transaction = await tronProvider.trx.getTransaction('transactionID');
  const signedTx = await tronProvider.trx.sign(transaction);
  console.log('Signed transaction:', signedTx);
  ```

### 3.3 Notes
- **Interface Assumption**: Without specific ABWallet Tron API details, it’s assumed to resemble TronLink’s TronWeb.
- **Reference**: TronLink integration documentation ([https://docs.tronlink.org/](https://docs.tronlink.org/)).
- **Network Selection**: Ensure the user selects the correct Tron network (e.g., Mainnet or Nile Testnet).

## 4. Connecting to Solana
Comming soon...

## 5. Additional Operations

### 5.1 Signing
- **EVM**: Use `personal_sign` or `eth_signTypedData_v4` for signing.
- **Tron**: Use `tronProvider.trx.sign` for transactions or messages.

### 5.2 Chain Selection
- **EVM**:
  ```javascript
  provider.request({
      method: 'wallet_switchEthereumChain',
      params: [{ chainId: '0x1' }]
  });
  ```
- **Tron**: Check or switch networks via `tronProvider` (refer to TronLink documentation).

### 5.3 Error Handling
Handle these cases:
- User rejection (error code 4001).
- Wallet not installed or `window.abwallet` not detected.
- Network mismatch or connection failures.

### 5.4 Security
- **No Private Keys**: DApps must not request or store private keys or mnemonics.
- **Secure Communication**: Use HTTPS for wallet interactions.
- **User Prompts**: Provide clear messages for user rejections or errors.

## 6. Summary

| Blockchain | Namespace                     | Connection Method                              | Reference Documentation                                                  |
|------------|-------------------------------|-----------------------------------------------|--------------------------------------------------------------------------|
| EVM        | `window.abwallet.ethereum`    | `provider.request({ method: 'eth_requestAccounts' })` | [MetaMask Documentation](https://docs.metamask.io/)                      |
| Tron       | `window.abwallet.tron`        | `tronProvider.request({ method: 'tron_requestAccounts' })` | [TronLink Documentation](https://docs.tronlink.org/)                     |


- **Detect ABWallet**: Use `isInABWalletApp()` to confirm the environment.
- **EVM**: Leverage `window.abwallet.ethereum` with MetaMask protocols.
- **Tron**: Use `window.abwallet.tron`, similar to TronLink.

## 7. Reference Resources
- MetaMask Developer Documentation: [https://docs.metamask.io/](https://docs.metamask.io/)
- TronLink Integration Documentation: [https://docs.tronlink.org/](https://docs.tronlink.org/)
- Solana Wallet Adapter Documentation: [https://github.com/solana-labs/wallet-adapter](https://github.com/solana-labs/wallet-adapter)
- Tron Developer Center: [https://developers.tron.network/](https://developers.tron.network/)
- Solana Developer Documentation: [https://solana.com/developers](https://solana.com/developers)
# Chain Configuration Guide for Amped Finance

## Currently Enabled Chains

### Mainnet Chains
- **146** - Orderly Network (Default)
- **1** - Ethereum Mainnet
- **8453** - Base
- **42161** - Arbitrum One
- **10** - Optimism
- **137** - Polygon

### Testnet Chains
- **84532** - Base Sepolia
- **421614** - Arbitrum Sepolia
- **11155420** - Optimism Sepolia
- **80002** - Polygon Amoy

## Available Chains from Orderly Network

### Additional Mainnet Chains You Can Enable
Add these chain IDs to `VITE_ORDERLY_MAINNET_CHAINS` in your `.env` file:

- **43114** - Avalanche C-Chain
- **56** - BNB Smart Chain
- **5000** - Mantle
- **59144** - Linea
- **534352** - Scroll
- **204** - opBNB
- **81457** - Blast
- **666666666** - Degen
- **7777777** - Zora

### Additional Testnet Chains
Add these to `VITE_ORDERLY_TESTNET_CHAINS`:

- **43113** - Avalanche Fuji
- **97** - BSC Testnet
- **5003** - Mantle Sepolia
- **59141** - Linea Sepolia
- **534351** - Scroll Sepolia

## How to Enable More Chains

### Step 1: Update Environment Variables
Edit your `.env` file and add the chain IDs separated by commas:

```env
# Example: Adding Avalanche, BSC, and Mantle to mainnet
VITE_ORDERLY_MAINNET_CHAINS=146,1,8453,42161,10,137,43114,56,5000

# Example: Adding more testnets
VITE_ORDERLY_TESTNET_CHAINS=84532,421614,11155420,80002,43113,97
```

### Step 2: Verify RPC Endpoints (Optional)
If you want to use custom RPC endpoints for specific chains, you can modify the wallet configuration. The Orderly SDK will use default RPC endpoints, but you can override them if needed.

### Step 3: Test the Configuration
1. Restart your development server:
   ```bash
   yarn dev
   ```

2. Check the wallet connection modal - you should see the new chains available

3. Try switching between chains in the wallet interface

## Important Notes

1. **Chain Support**: Not all chains may have full trading support on Orderly Network. The chains will appear in the wallet selector, but trading functionality depends on Orderly's backend support.

2. **Default Chain**: The `VITE_DEFAULT_CHAIN` sets which chain users start with. Make sure it's included in your enabled chains list.

3. **Network Switching**: When users switch between mainnet and testnet chains, the app will reload to switch network contexts.

4. **Wallet Compatibility**: 
   - EVM chains work with MetaMask, WalletConnect, and other EVM wallets
   - Solana support is separate and handled through Solana wallet adapters

5. **Performance**: Adding too many chains might make the chain selector UI cluttered. Consider your users' needs when selecting which chains to enable.

## Troubleshooting

### Chains Not Appearing
- Make sure chain IDs are comma-separated with no spaces
- Verify the chain IDs are correct (use chainlist.org for reference)
- Check browser console for any parsing errors
- Restart the development server after changes

### Wallet Connection Issues
- Some chains may require specific wallet configurations
- Ensure WalletConnect project ID is set if using WalletConnect
- Check that the chain is supported by the user's wallet

### Trading Not Working on New Chain
- Verify the chain is supported on Orderly Network's backend
- Check Orderly's documentation for chain-specific requirements
- Some chains may be display-only without full trading support

## Chain ID Reference

For a complete list of chain IDs and their details, visit:
- https://chainlist.org
- https://chainid.network

## Support

If you encounter issues with specific chains:
1. Check Orderly Network's official documentation
2. Verify the chain is listed in Orderly's supported networks
3. Test with both mainnet and testnet to isolate issues
4. Check the browser console for specific error messages
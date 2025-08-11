# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the Amped Finance perpetuals trading platform - a decentralized perpetual trading exchange built on Orderly Network. The platform is a customized fork of the Orderly Network broker template, built with Remix framework and deployable on Vercel.

## Core Development Commands

### Essential Commands
```bash
# Development
yarn dev                    # Start development server on http://localhost:5173

# Build & Production
yarn build                  # Build production version
yarn build:spa             # Build as SPA for GitHub Pages or static hosting
yarn preview               # Preview production build locally

# Code Quality
yarn lint                  # Run ESLint
yarn typecheck            # Run TypeScript type checking
```

## Architecture & Key Concepts

### Technology Stack
- **Framework**: Remix (SSR disabled, running as SPA)
- **UI Components**: Orderly Network SDK v2.5.2 (@orderly.network/*)
- **Authentication**: Privy integration for wallet connectivity
- **Wallets**: EVM (Ethereum, Base) and Solana wallet support
- **Styling**: Tailwind CSS with custom theme system
- **Deployment**: Vercel/GitHub Pages compatible

### Project Structure

```
app/
├── components/          # Custom components
│   ├── orderlyProvider/ # Main provider wrapping Orderly SDK
│   └── icons/          # Custom icon components
├── routes/             # Remix route files
│   ├── perp.$symbol.tsx    # Trading page for specific symbol
│   ├── portfolio.*.tsx     # Portfolio management pages
│   ├── markets.tsx         # Market overview
│   └── rewards.tsx         # Trading rewards pages
├── utils/              # Utility functions
│   ├── config.tsx      # Main configuration (menus, logos, PnL sharing)
│   ├── walletConfig.ts # Wallet configuration for different chains
│   └── seo.ts          # SEO and metadata configuration
└── styles/             # CSS files including theme.css
```

### Key Configuration Files

#### Environment Variables (.env)
Critical settings for the platform:
- `VITE_ORDERLY_BROKER_ID`: Broker identifier (amped)
- `VITE_ORDERLY_BROKER_NAME`: Display name
- `VITE_ORDERLY_MAINNET_CHAINS`: Supported mainnet chain IDs (146,1,8453)
- `VITE_ORDERLY_TESTNET_CHAINS`: Supported testnet chain IDs
- `VITE_ENABLED_MENUS`: Active navigation items
- `VITE_CUSTOM_MENUS`: External links in navigation
- `VITE_AVAILABLE_LANGUAGES`: Supported languages for i18n

#### OrderlyProvider Architecture
The OrderlyProvider (`app/components/orderlyProvider/index.tsx`) is the central component that:
1. Manages network selection (mainnet/testnet)
2. Configures wallet connectivity (Privy + WalletConnect)
3. Sets up i18n with dynamic language loading
4. Provides Orderly SDK context to entire app

### Routing System

The app uses Remix's file-based routing:
- `/` → Trading interface (redirects to `/perp/PERP_ETH_USDC`)
- `/perp/:symbol` → Trading page for specific perpetual
- `/portfolio/*` → Portfolio management sub-routes
- `/markets` → Market overview
- `/rewards/*` → Trading rewards and affiliate programs
- `/leaderboard` → Trading leaderboard

### Custom Features

#### Multi-Chain Wallet Support
The platform supports multiple blockchain networks:
- **Mainnet**: Orderly mainnet (146), Ethereum (1), Base (8453)
- **Testnet**: Base Sepolia (84532)
- Configured in `walletConfig.ts` with appropriate RPC endpoints

#### Dynamic Language Support
- Supports 16 languages with lazy loading
- Translation files in `public/locales/`
- Extended translations for custom UI elements in `public/locales/extend/`

#### Theme Customization
- Custom theme via `app/styles/theme.css`
- TradingView color configuration support
- Custom PnL sharing posters in `public/pnl/`

### Important Patterns

#### Symbol Management
- Default symbol: `PERP_ETH_USDC`
- Symbol persistence in localStorage
- Dynamic route updates when symbol changes

#### Network Switching
- Network ID stored in localStorage (`orderly_network_id`)
- Can be restricted via `VITE_DISABLE_MAINNET/TESTNET`
- Automatic chain configuration based on selected network

#### SEO Configuration
- Dynamic meta tags based on route
- Social media cards configuration
- Multi-language SEO support

### Testing Approach
The project doesn't have explicit test files but relies on:
- TypeScript for type safety
- ESLint for code quality
- Orderly SDK's built-in validation

### Deployment Notes

#### GitHub Pages Deployment
Use `yarn build:spa` which:
1. Sets up proper base paths for assets
2. Configures routing for SPA mode
3. Handles public path via `PUBLIC_PATH` env variable

#### Vercel Deployment
Standard `yarn build` works for Vercel with automatic configuration.

### Common Development Tasks

#### Adding New Trading Pairs
Trading pairs are fetched dynamically from Orderly Network API. No manual configuration needed.

#### Customizing Navigation
Edit `VITE_ENABLED_MENUS` and `VITE_CUSTOM_MENUS` in `.env` file.

#### Updating Theme
1. Visit Orderly Storybook theme editor
2. Export CSS
3. Replace content in `app/styles/theme.css`

#### Modifying Wallet Support
Edit `app/utils/walletConfig.ts` to add/remove chains or update RPC endpoints.

#### Language Management
- Add new language codes to `VITE_AVAILABLE_LANGUAGES`
- Ensure translation files exist in `public/locales/`

### API Integration

The platform uses Orderly Network's SDK which handles:
- WebSocket connections for real-time data
- REST API calls for trading operations
- TradingView chart data feeds
- Order management and execution

All API interactions are abstracted through the Orderly SDK components.
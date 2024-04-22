
# Interest Rate Model contest details

- Join [Sherlock Discord](https://discord.gg/MABEWyASkp)
- Submit findings using the issue page in your private contest repo (label issues as med or high)
- [Read for more details](https://docs.sherlock.xyz/audits/watsons)

# Q&A

### Q: On what chains are the smart contracts going to be deployed?
Ethereum mainnet, op-mainnet, op-sepolia
___

### Q: If you are integrating tokens, are you allowing only whitelisted tokens to work with the codebase or any complying with the standard? Are they assumed to have certain properties, e.g. be non-reentrant? Are there any types of <a href="https://github.com/d-xo/weird-erc20" target="_blank" rel="noopener noreferrer">weird tokens</a> you want to integrate?
We have an allowlist on the Auditor contract, and it should support standard ERC20-Tokens.
Tokens with a transfer fee are not supported.
___

### Q: Are the admins of the protocols your contracts integrate with (if any) TRUSTED or RESTRICTED? If these integrations are trusted, should auditors also assume they are always responsive, for example, are oracles trusted to provide non-stale information, or VRF providers to respond within a designated timeframe?
Chainlink is TRUSTED.
___

### Q: Are there any protocol roles? Please list them and provide whether they are TRUSTED or RESTRICTED, or provide a more comprehensive description of what a role can and can't do/impact.
Internal Roles are TRUSTED

deployer: timelock proposer, proxy admin of previewers.
protocol admin: timelock proposer, timelock executor, timelock canceller, PAUSER_ROLE.
timelock controller: DEFAULT_ADMIN_ROLE, TIMELOCK_ADMIN_ROLE, ProxyAdmin owner.
hypernative platform: EMERGENCY_ADMIN_ROLE.


DEFAULT_ADMIN_ROLE: able to set the configs of the markets, auditor and RewardsController. Can also grant and revoke roles. Can freeze/unfreeze markets.
PAUSER_ROLE: can pause and unpause markets.
EMERGENCY_ADMIN_ROLE: (can pause markets but can't unpause).
Timelock PROPOSER_ROLE: can propose to the timelock.
Timelock EXECUTOR_ROLE: can execute
Timelock TIMELOCK_ADMIN_ROLE: can grant and revoke timelock roles.
Timelock CANCELLER_ROLE: can cancel proposals.
Proxy admin: can upgrade contracts.
ProxyAdmin owner: can upgrade contracts with this singleton as their proxy admin.


___

### Q: For permissioned functions, please list all checks and requirements that will be made before calling the function.
All the setters in the protocol check for the DEFAULT_ADMIN_ROLE.
___

### Q: Is the codebase expected to comply with any EIPs? Can there be/are there any deviations from the specification?
The Markets is optional compliant with ERC-4626 following the standard for floating deposits.
___

### Q: Are there any off-chain mechanisms or off-chain procedures for the protocol (keeper bots, arbitrage bots, etc.)?
We have a liquidation bot that monitors the health of the protocol's accounts and calls the liquidate function.
___

### Q: Are there any hardcoded values that you intend to change before (some) deployments?
No.
___

### Q: If the codebase is to be deployed on an L2, what should be the behavior of the protocol in case of sequencer issues (if applicable)? Should Sherlock assume that the Sequencer won't misbehave, including going offline?
We assume the sequencer won't misbehave.
___

### Q: Should potential issues, like broken assumptions about function behavior, be reported if they could pose risks in future integrations, even if they might not be an issue in the context of the scope? If yes, can you elaborate on properties/invariants that should hold?
Yes.
___

### Q: Please discuss any design choices you made.
n/a
___

### Q: Please list any known issues/acceptable risks that should not result in a valid finding.
We trust Chainlink, and no liveness checks are performed while retrieving Oracle data.

___

### Q: We will report issues where the core protocol functionality is inaccessible for at least 7 days. Would you like to override this value?
No.
___

### Q: Please provide links to previous audits (if any).
https://github.com/exactly/audits
___

### Q: Please list any relevant protocol resources.
https://docs.exact.ly/

Price Feeds: https://docs.exact.ly/guides/price-feeds
___

### Q: Additional audit information.
n/a
___



# Audit scope


[protocol @ eb0a9f70fa9e4cdb99847ce5f0587611e8f4c077](https://github.com/exactly/protocol/tree/eb0a9f70fa9e4cdb99847ce5f0587611e8f4c077)
- [protocol/contracts/Auditor.sol](protocol/contracts/Auditor.sol)
- [protocol/contracts/InterestRateModel.sol](protocol/contracts/InterestRateModel.sol)
- [protocol/contracts/Market.sol](protocol/contracts/Market.sol)
- [protocol/contracts/MarketETHRouter.sol](protocol/contracts/MarketETHRouter.sol)
- [protocol/contracts/PriceFeedDouble.sol](protocol/contracts/PriceFeedDouble.sol)
- [protocol/contracts/PriceFeedPool.sol](protocol/contracts/PriceFeedPool.sol)
- [protocol/contracts/PriceFeedWrapper.sol](protocol/contracts/PriceFeedWrapper.sol)
- [protocol/contracts/RewardsController.sol](protocol/contracts/RewardsController.sol)
- [protocol/contracts/periphery/EXA.sol](protocol/contracts/periphery/EXA.sol)
- [protocol/contracts/periphery/EscrowedEXA.sol](protocol/contracts/periphery/EscrowedEXA.sol)
- [protocol/contracts/periphery/InstallmentsRouter.sol](protocol/contracts/periphery/InstallmentsRouter.sol)
- [protocol/contracts/utils/FixedLib.sol](protocol/contracts/utils/FixedLib.sol)


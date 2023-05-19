# Smart contract gas optimization

- uint8 saves gas than uint256
- Avoid loops
- Since, there are no floating points in solidity, use decimals to handle it. Beware that in division, Num>Den
- public state variables consume gas
- Extra text in return consumes gas 
- Events can be used to read variables which are only needed to be read by developer, not the user







# Smart contract security

- Use CEI withdrawal pattern(Check, Effects and Interaction) to prevent reentrancy


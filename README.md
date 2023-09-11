# Hedera Capstone Project expansion
Stackup bounty project - Car Borrowing DApp

## Feature Implemented

I have added a feature so that the Merchant can set an asking Price for the Car and can display it on the borrowing page, I had to make changes in the original smart contract to add a public mapping (int64=>uint256) called mintingPrices which takes an Nft serial number as key and assigns the minting price as its value. Since it is public, we can call it on the frontend using mingingPrices(serial_number) function call. It returns a promise which has a _hex propery which contains a hex value which can be converted to decimal value to get our minting price.
Another change made in the original smart contract is in the mintNft function where we are passing the 'mintPrice' from the Merchant as one of the arguments. After successul minting of the NFT, we then use the assignment,

mintingPrices[serial[0]] = mintPrice

which sets our custom mintPrice argument as the value for the NFT serial number key inside our mapping.

Changes were also made in the borrowing and returning functions to use the new mintPrice instead of the default lockupAmount by using the 'serial' argument passed to the function to call the mintingPrices mapping to get the custom price.

In the frontend, a new input field was added in the CreateCar component to add the custom price. This value was then passed onto createCar() function which calls the mintNFT with this argument. On the borrowCar function, in the transcatiion for the value, this custom price is used. Also in the BorrowCar page component, added an extra field to fetch the custom price and show it.

Originally, I had decided to implement three features but was only able to implement the above one. I had plans to add a burn function to remove a car and another mapping which stores an array of previous Owners. But Hedera Testnet hasn't been working properly for myself since 10-09-23, not allowing me to deploy new smart contracts. The contract reverts at the constructor() function provided in the quest which was unchanged by me. I checked by adding a custom message inside the revert() function in constructor(). I tried to ask for help in discord helpdesk for quest 8 but to no avail. Luckily I had deployed earlier a smart contract with the one feature mentioned above for testing the feature and was able to use it now.

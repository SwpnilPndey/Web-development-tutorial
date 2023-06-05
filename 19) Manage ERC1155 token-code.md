1. ERC 1155 tokens give extra flexibility in terms of NFT ownership. So, users can hold multiple copies of same NFT

2. First of all, all NFT images are uploaded to IPFS using JS or GUI software like Pinata or NFT storage

NFTs should be named 00001.png, 00002.png etc for 30000 NFTs (decimal places) 

3. Create and upload NFT metadata.json for each image using JS using following code

var fs = require('fs');

for (var i = 0; i < 30000 ; i++) { // for five images
  var json = {}
  json.name = "Token #" + i;
  json.description = "This is the description for token #" + i;
  json.image = "ipfs://bafybeiezpnn5ycnqg25piopx2efjcy4zoydbrwe4fghafsakuziiuibonq/" + i + ".png";

  fs.writeFileSync('imagejson/' + i+'.json', JSON.stringify(json));
}

### Here, the ipfs CID is the CID of the image folder uploaded on ipfs

### To view the JSON on browser, go to : http://ipfs.io/ipfs://bafybeiezpnpiopx2efjcy4zoydbrwe4fghafsakuziiuibonq/metadata.json



4. Mint NFTs from NFT marketplace

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

import "@openzeppelin/contracts/token/ERC1155/ERC1155.sol";
import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts/security/Pausable.sol";
import "@openzeppelin/contracts/token/ERC1155/extensions/ERC1155Supply.sol";
import "@openzeppelin/contracts/utils/Strings.sol";


contract HAWKSNFT is ERC1155, Ownable, Pausable, ERC1155Supply {

   // Exclusion of name and symbol is intentional as it is a more flexible NFT collection standard.
	
    uint256 public mintingFee;
    uint256 public maxSupply;
    constructor()
        ERC1155("ipfs://bafybeiezpnn5ycnqg25piopx2efjcy4zoydbrwe4fghafsakuziiuibonq/"){ 
// CID of metadata files
            mintingFee=0.001*10**18; // 0.5 USDT
            maxSupply=30000;
        }

    function setURI(string memory newuri) public onlyOwner {
        _setURI(newuri);
    }

    function pause() public onlyOwner {
        _pause();
    }

    function unpause() public onlyOwner {
        _unpause();
    }

    function mint( uint256 id, uint256 amount) public payable {
        require(id==0,"ID entered is not a valid NFT");
        require(msg.value>=mintingFee*amount,"Not enough fees paid");
        require(totalSupply(id)+amount<=maxSupply,"Maximum NFTs already minted");
        _mint(msg.sender, id, amount, "");
    }

    function mintBatch(address to, uint256[] memory ids, uint256[] memory amounts, bytes memory data)
        public
        onlyOwner
    {
        _mintBatch(to, ids, amounts, data);
    }

     function uri(uint256 iD) public view virtual override returns (string memory) {
        require(exists(iD),"URI doesnot exist");
        return string(abi.encodePacked(super.uri(iD),Strings.toString(iD),".json"));//convert number to string
    }

    function _beforeTokenTransfer(address operator, address from, address to, uint256[] memory ids, uint256[] memory amounts, bytes memory data)
        internal
        whenNotPaused
        override(ERC1155, ERC1155Supply)
    {
        super._beforeTokenTransfer(operator, from, to, ids, amounts, data);
    }


     receive() external payable {}

     function withdraw() public onlyOwner {
        payable(msg.sender).transfer(address(this).balance);
     }
}


5. Create a NFT marketplace where users can buy and sell these NFTs

// SPDX-License-Identifier: MIT
pragma solidity <=0.8.9;

import "@openzeppelin/contracts/token/ERC1155/IERC1155.sol";

import "@openzeppelin/contracts/access/Ownable.sol";

import "@openzeppelin/contracts/token/ERC1155/utils/ERC1155Holder.sol";

contract NFTMarketplace is Ownable, ERC1155Holder {
    IERC1155 public nftContract;

    struct Listing {
        uint256 tokenId;
        address seller;
        uint256 price;
        bool active;
    }

    mapping(uint256 => Listing) public listings;

    event NFTListed(uint256 indexed tokenId, address indexed seller, uint256 price);
    event NFTSold(uint256 indexed tokenId, address indexed buyer, uint256 price);

    constructor(address _nftContract) {
        nftContract = IERC1155(_nftContract);
    }

    function listNFTForSale(uint256 tokenId, uint256 price) external {
        require(nftContract.balanceOf(msg.sender, tokenId) > 0, "You don't own this NFT");
        require(listings[tokenId].active == false, "NFT is already listed");
        
        nftContract.safeTransferFrom(msg.sender, address(this), tokenId,1, ""); // 1 quantity NFT
        
        listings[tokenId] = Listing(tokenId, msg.sender, price, true);
        emit NFTListed(tokenId, msg.sender, price);
    }

    function buyNFT(uint256 tokenId) external payable {
        Listing storage listing = listings[tokenId];
        require(listing.active == true, "NFT is not listed for sale");
        require(msg.value >= listing.price, "Insufficient funds");

        address seller = listing.seller;
        listing.active = false;
        delete listings[tokenId];

        nftContract.safeTransferFrom(address(this), msg.sender, tokenId, 1, "");
        payable(seller).transfer(msg.value);

        emit NFTSold(tokenId, msg.sender, listing.price);
    }
        
    }



## This way, ERC 1155 NFT tokens are handled 
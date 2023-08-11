1. For ERC 721, the common way of minting NFT is that any user can upload his media to IPFS and mint that NFT media to his name

- Upload to IPFS using JS and retrieve the CID of the image

- Use this CID to create metadata.json file

- Upload this json to IPFS. This URI of the metadata becomes the tokenURI which user needs to enter while using NFT minting smart contract to mint NFT media whose metadata.json has been uploaded, to his account address


2. Now, NFT minting service provider creates following contract : 


// SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/token/ERC721/extensions/ERC721Enumerable.sol";
import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";
import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts/utils/Counters.sol";

contract MyToken is ERC721, ERC721Enumerable, ERC721URIStorage, Ownable {
    using Counters for Counters.Counter;

    Counters.Counter private _tokenIdCounter;

    constructor() ERC721("MyToken", "MTK") {}

    function _baseURI() internal pure override returns (string memory) {
        return "ipfs://bafybeiezpnn5ycnqg25piopx2efjcy4zoydbrwe4fghafsakuziiuibonq/";
    }

    function safeMint(address to, string memory uri) public onlyOwner {
        uint256 tokenId = _tokenIdCounter.current();
        _tokenIdCounter.increment();
        _safeMint(to, tokenId);
        _setTokenURI(tokenId, uri);
    }

    // The following functions are overrides required by Solidity.

    function _beforeTokenTransfer(address from, address to, uint256 tokenId, uint256 batchSize)
        internal
        override(ERC721, ERC721Enumerable)
    {
        super._beforeTokenTransfer(from, to, tokenId, batchSize);
    }

    function _burn(uint256 tokenId) internal override(ERC721, ERC721URIStorage) {
        super._burn(tokenId);
    }

    function tokenURI(uint256 tokenId)
        public
        view
        override(ERC721, ERC721URIStorage)
        returns (string memory)
    {
        return super.tokenURI(tokenId);
    }

    function supportsInterface(bytes4 interfaceId)
        public
        view
        override(ERC721, ERC721Enumerable, ERC721URIStorage)
        returns (bool)
    {
        return super.supportsInterface(interfaceId);
    }
}


### Here base URI is same for all tokens. It means while uploading the metadata.json files to IPFS, every user has to mandatorily upload metadata.jsons to same base URI. 

### For example, one user uploads NFT metadata file as : MYNFT.json to a base URI : 
### "ipfs://bafybeiezpnn5ycnqg25piopx2efjcy4zoydbrwe4fghafsakuziiuibonq/MYNFT.json"

### So, while minting NFT this way, while using the **safeMint** function, the tokenURI is MYFT.json and not the complete URI for the NFT



3. Once NFT is minted to any user's address, it stays there till the token is sold at the NFT marketplace


4. A simple NFT marketplace contract looks like below : 


// SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

import "@openzeppelin/contracts/token/ERC721/IERC721.sol";
import "@openzeppelin/contracts/token/ERC721/utils/ERC721Holder.sol";
import "@openzeppelin/contracts/utils/Address.sol";

contract Marketplace is ERC721Holder {
    using Address for address payable;

    struct Listing {
        address seller;
        uint256 tokenId;
        uint256 price;
        bool isActive;
    }

    mapping(uint256 => Listing) private listings;

    IERC721 private nftContract;

    constructor(address _nftContract) {
        nftContract = IERC721(_nftContract);
    }

    function listNFTForSale(uint256 tokenId, uint256 price) external {
        require(!listings[tokenId].isActive, "NFT already listed");
        require(nftContract.ownerOf(tokenId) == msg.sender, "Not the owner of the NFT");

        nftContract.safeTransferFrom(msg.sender, address(this), tokenId);
        listings[tokenId] = Listing(msg.sender, tokenId, price, true);
    }

    function buyNFT(uint256 tokenId) external payable {
        Listing memory listing = listings[tokenId];
        require(listing.isActive, "NFT is not listed");
        require(msg.value >= listing.price, "Insufficient payment");

        delete listings[tokenId];
        nftContract.safeTransferFrom(address(this), msg.sender, tokenId);
        payable(listing.seller).sendValue(listing.price);
    }
}


### The advantage of creating NFTs with consecutive token IDs is the ease in buying and selling NFTs on a marketplace


## This way, ERC 721 NFT tokens are handled 
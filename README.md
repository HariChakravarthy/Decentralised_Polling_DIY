# Decentralized-Polling
# Decentralized-Polling
# DecentraPoll DApp - Changes Overview

This document concludes the key changes and improvements made between the initial and final stages of the **DecentraPoll DApp**.

*Initial* : Basic Polling Functionality
Features:

Wallet Connection:

Connects to MetaMask on app load.

Displays the user's Ethereum wallet address.

Poll Display:

Fetches and displays active polls from the smart contract.

Poll details include the question, options, vote counts, and total votes.

Smart Contract Interaction:

Read-only: no support for poll creation or voting.

Key Limitations:

--- No limit on poll creation.

--- No mechanism to handle repeated voting.

--- Static time display – no timestamps shown.

--- Deactivate a specific poll 

*Final* : Feature-Rich Interactive Polling

Features Added by Hari:

1. Limit Number of Polls Per User

mapping(address => uint256) public pollsCreated;
uint256 public MAX_POLLS_PER_USER = 1;

when i try to create the second poll it will display failed to create the poll i uploaded the screenshot of that .

require(pollsCreated[msg.sender] < MAX_POLLS_PER_USER, "Poll limit reached");
pollsCreated[msg.sender]++;

2. Show Time Since Poll Was Created

Solidity  : 
createdAt: block.timestamp

React : 
function timeSince(timestamp) {
  const seconds = Math.floor((Date.now() / 1000) - timestamp);
  ...
}

3. Disable Vote Button if User Has Already Voted

Solidity  : 
require(!hasVoted[msg.sender][_pollId], "You have already voted");

React : 
const voted = await contract.hasUserVoted(account, pollId);
if (poll.hasVoted) return <p>You've already voted</p>;

4. Deactivate a Specific Poll

Added the function in Solidity 
function deactivatePoll(uint256 _pollId) public {
    require(polls[_pollId].creator == msg.sender, "Only creator can deactivate");
    require(polls[_pollId].active, "Poll is already inactive");
    polls[_pollId].active = false;
}

// Changes I made in the given Dapp

Differences are made according to the project guidelines solidity and react Core Functionality changes 

Feature				Initially 		Finally (My Addition)

Poll Creation			Not available		Users can create polls
Poll Deactivation		Not available		Creator can deactivate
Limit Polls Per User		Not implemented		One poll per user (modifiable limit)
Poll Timestamp & Time Since	Not shown		createdAt with relative time display
Vote Button Behavior		Always visible		Hidden if already voted
Poll Voting			Not available		Vote with checks and alerts

*Conclusion* :
From the given DIY blockchain project I conclude the following ,
The given DecentraPoll DApp is evolved from a basic read-only DApp into a secure, user-interactive voting system with proper poll. With features like poll limits, vote prevention, and time tracking, the application is now user-friendly.




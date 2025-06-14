# Experiment 2: Blockchain-Based Crowdfunding (Kickstarter Alternative)
## Name   : LOKESH KHANNA R
## Reg no : 212222040088
## Aim:
To create a decentralized crowdfunding platform where donors contribute funds only if the campaign goal is met.

## Algorithm:
1.The project creator deploys a crowdfunding smart contract with a funding goal and deadline.

2.Contributors send ETH to the contract before the deadline, and their contributions are recorded.

3.The contract tracks the total amount raised during the campaign.

4.If the goal is met before the deadline, the creator can withdraw the funds.

5.If the goal is not met, contributors can claim refunds after the deadline.

## Program:
```py
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Crowdfunding {
    struct Campaign {
        address creator;
        uint256 goal;
        uint256 deadline;
        uint256 amountRaised;
        bool goalMet;
        mapping(address => uint256) contributions;
    }

    Campaign public campaign;

    constructor(uint256 _goal, uint256 _duration) {
        campaign.creator = msg.sender;
        campaign.goal = _goal;
        campaign.deadline = block.timestamp + _duration;
    }

    function contribute() public payable {
        require(block.timestamp < campaign.deadline, "Campaign ended");
        campaign.amountRaised += msg.value;
        campaign.contributions[msg.sender] += msg.value;
    }

    function withdrawFunds() public {
        require(msg.sender == campaign.creator, "Only creator can withdraw");
        require(campaign.amountRaised >= campaign.goal, "Goal not met");
        payable(msg.sender).transfer(campaign.amountRaised);
        campaign.goalMet = true;
    }

    function refund() public {
        require(block.timestamp > campaign.deadline, "Campaign still active");
        require(campaign.amountRaised < campaign.goal, "Goal was met");
        uint256 amount = campaign.contributions[msg.sender];
        campaign.contributions[msg.sender] = 0;
        payable(msg.sender).transfer(amount);
    }
}
```
# Expected Output:
![image](https://github.com/user-attachments/assets/15d635bf-7749-4fe6-9077-e7ce06af4f67)

Users can contribute ETH to the campaign.
If the goal is met, the creator can withdraw funds.
If the goal is not met, contributors can claim a refund.

# High-Level Overview:
Teaches decentralized fundraising.


Avoids fraud by ensuring funds are only transferred if the goal is met.

# RESULT: 
The crowdfunding smart contract was successfully implemented to securely manage donations, ensuring funds are released only if the campaign goal is met.

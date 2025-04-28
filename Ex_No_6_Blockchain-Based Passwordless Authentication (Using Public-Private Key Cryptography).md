# Experiment 6: Blockchain-Based Passwordless Authentication (Using Public-Private Key Cryptography)
## Name:M Sathish kumar
## Reg no:212222040150
## Date:23/4/25


# Aim:
To implement a secure passwordless authentication system using public-private key cryptography on Ethereum. This prevents phishing and password leaks.

# Algorithm:
Step 1: 
User Registration
A user registers with their Ethereum public key (instead of a password).
Step 2: Login Process
When logging in, the user signs a random challenge message using their private key.
The smart contract verifies the signature using the user’s public key.
# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PasswordlessAuth {
    mapping(address => bool) public registeredUsers;

    event UserRegistered(address user);
    event UserAuthenticated(address user);

    function registerUser() public {
        require(!registeredUsers[msg.sender], "Already registered");
        registeredUsers[msg.sender] = true;
        emit UserRegistered(msg.sender);
    }

    function authenticate(bytes32 hash, uint8 v, bytes32 r, bytes32 s) public view returns (bool) {
        require(registeredUsers[msg.sender], "User not registered");
        address signer = ecrecover(hash, v, r, s);
        return signer == msg.sender;
    }
}
```

# Expected Output:
Users can register without a password.
![image](https://github.com/user-attachments/assets/56b4d5b0-29e4-4c06-9587-580d11e01682)


Users sign a challenge with their private key for authentication.
![image](https://github.com/user-attachments/assets/071ac3ed-5fd1-4973-a356-7bc616a580e4)


The smart contract verifies signatures to confirm identity.

![image](https://github.com/user-attachments/assets/0cb4a1a6-258d-46f8-8191-e0d78774deae)


# High-Level Overview:
Eliminates password hacks & phishing attacks.
Uses Ethereum's built-in cryptographic functions.
Inspired by Web3 login solutions like MetaMask authentication.

# RESULT: 
Thus,Blockchain-Based Passwordless Authentication (Using Public-Private Key Cryptography) has been created and successfully executed.

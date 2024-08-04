### [S-#] Storing the Password on-chain makes it visible to everyone and its no longer private

** Description: **

All data stored on-chain is visible to anyone, and can be read directly from blockchain. The PasswordStore::`s_password` variable is intended to be a private variable an only accessed through PasswordStore::`getPassword` function, which intended to be only called by the owner contract

We show one such method of reading any data off-chain below.

** Impact: **

Anyone can read the private password, severly breaking the functionality of the protocol.

** Proof of Concept: **

** Recommended Mitigation: **


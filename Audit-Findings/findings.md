### [S-#] Storing the Password on-chain makes it visible to everyone and its no longer private

** Description: **

All data stored on-chain is visible to anyone, and can be read directly from blockchain. The PasswordStore::`s_password` variable is intended to be a private variable an only accessed through PasswordStore::`getPassword` function, which intended to be only called by the owner contract

We show one such method of reading any data off-chain below.

** Impact: **

Anyone can read the private password, severly breaking the functionality of the protocol.

orage tool

We use `1` because that's the storage slot of `s_password` in the contract.

```
cast storage <ADDRESS_HERE> 1 --rpc-url http://127.0.0.1:8545
```

You'll get an output that looks like this:

`0x6d7950617373776f726400000000000000000000000000000000000000000014`

You can then parse that hex to a string with:

```
cast parse-bytes32-string 0x6d7950617373776f726400000000000000000000000000000000000000000014
```

And get an output of:

```
myPassword
```

** Recommended Mitigation: ** Due to this, the overall architecture of the contract should be rethought. One could encrypt the password off-chain, and then store the encrypted password on-chain. This would require the user to remember another password off-chain to decrypt the password. However, you'd also likely want to remove the view function as you wouldn't want the user to accidentally send a transaction with the password that decrypts your password. 




# Fix SSH Login `Too many authentication failures` Due To Multiple SSH Keys

When loging in to your one of your remote server with or without a password and you got the `Too many authentication failures` error, then its your ssh client using multiple irrelivant keys for authentication. There are two ways to get out from this. One: Explicitly indicate you're using password as your method of authentication, if you're using one. Or, Two: specify SSH to use only relevant identity.

## Specific Authentication Method Using Password Only

`ssh -o 'PreferredAuthentications password' user@someserver.com`

## Use Identity Only

`ssh -o 'IdentitiesOnly yes' user@someserver.com`

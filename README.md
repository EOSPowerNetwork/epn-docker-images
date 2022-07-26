# Description

Better organization for EPN-related docker endeavors.

# Encoding

Directories containing docker images are prefixed with an encoding scheme that identifies the entire dependency tree.

The number in the prefix identifies what layer image it is in the tree. The character after the number indicates what image variant it is at that layer. The first letters of the prefix indicates the image variant at each of the prior layers.

## Todo

- Extract a common root docker image between 0a and 0b
- Delete the vscode-open-system-epn project in favor of pointing at a docker image built by this eosio-epn-clsdk docker image.
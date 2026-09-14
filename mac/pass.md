# `pass` Command on Mac

The pass command is a Unix standard secrets manager that uses simple file and directory structure to save secret values that are encrypted at rest.

## Installation

If using Homebrew, install the following packages: `brew install pass gnupg pinentry-mac`

PinEntry needs some additonal setup. Edit the gpg-agent file at `~/.gnupg/gpg-agent.conf` with the following (specifically for M-series AND homebrew install): `echo "pinentry-program /opt/homebrew/bin/pinentry-mac" >> ~/.gnupg/gpg-agent.conf`

Also modify your `~/.zshrc` to tell GPG where to send TTY prompts: `echo 'export GPG_TTY=$(tty)' >> ~/.zshrc`

Then restart the agent: `gpgconf --kill gpg-agent`

Retrieve the new GPG key ID: `gpg --list-secret-keys --keyid-format LONG

The key ID you are looking for is on the `sec` line, after the `ed25519/` and before the space character, should be 16 characters long

Initialize the pass store: `pass init <your_key_id>`

Verify the empty pass store (output should be `Password Store` with no additional lines): `pass ls`

### Configure TouchID

If you are tired of using the passphrase, you can setup TouchID for biometric unlocks.

Install custom tap: `brew tap jorgelbg/tap`

Install the package: `brew install pinentry-touchid`

[X] ERROR: Turns out this tap is super old and doesn't work on the newest Homebrew/MacOS version... big sad

## CRUD Actions

### Create

Add a single line value: `pass insert github/password`

Since everything is a tree, you can nest secrets however you want: `pass insert services/personal/huggingface/token`

Multiline secret values: `pass insert -m services/aws/credentials`

Generate a random password automatically (last argument is secret length as an integer): `pass generate google/password 20`

### Read

Print password to stdout in terminal: `pass show google/password`

Copy to clipboard (auto-cleared after 45 seconds): `pass -c github/password`

### Update

You can overwrite a secret value: `pass insert google/password`

You can skip the confirmation prompt by using the `f` flag: `pass insert -f google/password`

For multiline secrets that require an interactive prompt: `pass edit services/aws/credentials`

To generate a new random password for an existing secret: `pass generate -f google/password 24`

### Delete

Remove a single secret: `pass rm google/password`

Remove secret without confirmation prompt: `pass rm -f google/password`

Remove an entire directory of secrets: `pass rm -r services/github`

## Modifying Secret Trees

Since `pass` is based on standard files and directories, it uses the standard Linux conventions for moving and renaming parts of the secret tree.

Rename a secret: `pass mv github/token github/specific-token`

Move a sub-tree: `pass mv services/aws cloud/aws`

## Git Integration

Another benefit of the simple file/directory foundation: there is built-in Git integration for all actions. Commits will use standard messages for each change. Changes can be pushed to a remote backup using `pass git push`.


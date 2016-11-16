# Much less pass

Inspired by the [LessPass](http://github.com/lesspass) project.

This project uses Python's `pbkdf2_hmac` function to derive a key based on the
service, login and a master password that is then rendered in ASCII characters
and that can be used as a password online.

As the master password is used as the initial salt of the computation, it is
recommended to use a long passphrase.

You'll want to ensure your shell is configured *not* to record lines starting
with a space.


# Usage

    $ much-less-pass --service=github.com --login=rob@example.com


# Command-line arguments

List of compulsory arguments to feed the key derivation algorithm:

- `--service=`: for example `github.com`,
- `--login=`: for examle rob@example.com.

List of arguments controlling key derivation:

- `--iter=656000`: number of rounds for the algorithm.

List of arguments controlling key representation:

- `--length=32`: length of key representation,
- `-l`: disable lowercase characters,
- `-u`: disable uppercase characters,
- `-d`: disable digits characters,
- `-p`: disable puncutation characters.

Additionally, it's possible to read arguments from a file; in that case, the
service name is derived from the filename.

Given this input file:

    $ cat ~/.much-less-pass/github.com
    --length=64 --login=rob@example.com

Using it as follows:

    $ much-less-pass -r ~/.much-less-pass/github.com
    rob@example.com / github.com: GENERATED_KEY_REPRESENTATION

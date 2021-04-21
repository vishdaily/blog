---
title: All about GPG keys
layout: post
tags:
  - gpg
  - linux
---

# FAQ Commands

```bash
# https://www.gnupg.org/
gpg --gen-key
gpg --verify &lt;key&gt;
gpg --edit-key testing@gmail.com
&gt;&gt;&gt;&gt; fpr
&gt;&gt;&gt;&gt; sign
&gt;&gt;&gt;&gt; check
gpg --fingerprint
gpg --list-keys
gpg --list-secret-keys
gpg --full-generate-key
gpg --export -o testing.pub -r testing@gmail.com
gpg -o 1 1.raw
gpg --yes 11.raw
gpg --change-passphrase testing@gmail.com
gpg --export --armor -o "testing@gmail.com.pubring.gpg" -rtesting@gmail.com
gpg --armor -o "testing@gmail.com.privring.gpg" --export-secret-key testing@gmail.com
gpg --output doc.gpg --encrypt --recipient blake@cyb.org doc
gpg --output doc --decrypt doc.gpg
gpg --output doc.gpg --symmetric doc
gpg --import testing\@gmail.com.pubring.gpg
```

# Extend an expired subkey

```bash
gpg --list-keys
gpg --edit-key <key>
> key <1> # index of first sub key.  this wil put * after the word sub
> expire
> # select the expire date
> save
```
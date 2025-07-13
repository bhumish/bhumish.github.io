---
title: "Simplyhash Python Utility"
date: 2013-09-30
draft: false
description: "A Python module for generating hashes using various algorithms including MD5, SHA1, SHA256, and SHA512, with interactive input options for files or strings"
tags: ["python", "hash", "cryptography", "utility", "md5", "sha1", "sha256", "sha512", "pypi"]
categories: ["Programming", "Python", "Utilities"]
---

After developing a tiny game of Rock Paper Scissors Lizard Spock based on python, during the free time today I made a module for getting the hash of a user provided string. This hash function makes use of the built-in 'hashlib' in Python, and provides options for using any of the hash function among md5 (128 bits), sha1 (160 bits), sha256 (256 bits) and sha512 (512 bits). It is kind of interactive, and can take any of the two inputs – either a file or a string. Unless specified, the program continues to give the hash through the chosen function.

I am willing to add more hash functions (like RIPEMD, md6, whirlpool) in the next update. Plus, thoughts of some encryption mixology module are in progress.

Have uploaded the hash-er module here: [simplyhash.py on PyPI](https://pypi.python.org/pypi/simplyhash/1.0.1)
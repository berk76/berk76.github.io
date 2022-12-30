---
title: Simple password manager for my Python projects
date: 2021-10-05 21:00:00 +0100
categories: [programming]
tags: [python]
---

Sometime I am creaing Python scripts for various purposes. My trouble is that scripts often need credentials and I have to be careful to not commit credentials into repository and/or put credentials back to my script when I want to use it. So I have decided to create simple password manager for my scripts.

Idea was very simple - to create Python package which will keep credentials in vault in my home directory. Python script will just ask "give me credentials for named project" and password manager will read and provide them back or prompt credentials if they don't exist and save them in vault. Usage should be as simple as possible and ideally vault is encrypted.

Result is here and usage is really simple. First you need to install mypwd package.

 
 ```sh
 pip install mypwd

 ```

And now you can use it in your script.

```python
import mypwd

# get credentials for mongo-dev project from vault
login, password, server = mypwd.get_values("mongo-dev", ["login", "password", "server"])

#use credentials in mongodb uri string
uri = f"mongodb://{login}:{password}@{server}/admin?retryWrites=true&w=majority"
```

What all parameters will be in array is up to you. If credentials are missing in your vault password manager will simply prompt them and store them in vault.

Vault is json file stored in `$HOME/mypwd.json` and here is example how it may look like.

```json
{
  "mongo-uat": {
    "login": "appl",
    "password": "hS78#pbTgc#J.CQL",
    "server": "myserver-uat.com"
  },
  "mongo-dev": {
    "login": "appl",
    "password": "VacK>p3k3~t*c~RX",
    "server": "myserver-dev.com",
    "note": "Valid until end of month"
  }
}
```

You can encrypt vault with your `gpg` key and password manager will work with this encrypted version.

```sh
mypwd encrypt -e your.email@something.com
```

In case you needed decrypt it manually you can use following command.

```sh
mypwd decrypt
```

I know, encryption using gpg is a bit cumbersome but it works fine.

Visit project in [GitHub](https://github.com/berk76/mypwd)

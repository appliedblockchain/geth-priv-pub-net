# Creatign a docker-compose.yml with istanbul-tools
## Installing istanbul-tools

Install go: https://golang.org/dl/

Install the actual tool: `go get github.com/getamis/istanbul-tools/cmd/istanbul`

This will install it under your $GOPATH, so in order to be able to use `istanbul` you need to make sure `$GOPATH/bin` is in your `$PATH`

Now if you type `istanbul`, you should see:

```sh
NAME:
   istanbul - the istanbul-tools command line interface

USAGE:
   istanbul [global options] command [command options] [arguments...]

VERSION:
   v1.0.0

COMMANDS:
     extra    Istanbul extraData manipulation
     setup    Setup your Istanbul network in seconds
     help, h  Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --help, -h     show help
   --version, -v  print the version

COPYRIGHT:
   Copyright 2017 The AMIS Authors
```


## Generating a config:

``` sh
istanbul setup --num 4 --docker-compose --save
docker-compose up
```

## Creating an account
1. Install geth
2. `geth attach http://localhost:8545`
3. Run `personnal.newAccount`, enter a password
4. log into validator-0 container and retrieve the account
5. modify docker-compose to include that file in validator-0
6. modify docker-compose to give eth to the new account in the genesis block(for each nodes)
7. modify docker-compose to unlock at start up(`--unlock '0' --password '/eth/password.txt'`)
8. if you want the chain data to persist, add a volume for each validator and map it to `/eth` in each validator(or node)

You can look at docker-compose.yml for the end result.

# Running the demo

1. npm install
2. npm run compile
3. node deploy.js
4. node index.js
# Node and npm

Check installed version of **node**:

```shell
$ node -v
```

Check installed version of **npm**:

```shell
$ npm -v
```

Check installed version of **nvm**:

```shell
$ nvm -v
```

## NVM

Install **nvm**:

```shell
$ sudo dnf install -y gcc-c++ make
$ curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
```

## Node

Install **node** version you need:

```shell
$ nvm install v18.16.0
```

Install the latest LTS release of Node.js:

```shell
$ nvm install --lts
```

List all available versions to install:

```shell
$ nvm ls-remote
```

## NPM

Install the latest version:

```shell
$ npm install -g npm@latest
```

## [npmjs](https://www.npmjs.com)

To add user for logging in [npmjs](https://www.npmjs.com) 

```shell
$ npm adduser
```

and follow the instructions in the browser.

Publish package:

```shell
$ npm publish
```

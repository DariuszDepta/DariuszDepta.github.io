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
Or install **nvm**:

```shell
$ sudo dnf install -y gcc-c++ make
$ curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
```

Install **node** version you need:
```shell
$ nvm install v18.16.0
```

Install the latest LTS release of Node.js:
```shell
nvm install --lts
```

Check installed versions of **node** and **npm**:

```shell
$ node -v
v18.17.0
$ npm -v
9.6.7
```

To add user for logging in [npmjs](https://www.npmjs.com) 

```shell
$ npm adduser
```
and follow the instructions in the browser.

Publish:

```shell
$ npm publish
```

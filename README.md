# npm-pkgr

[![Build Status](http://img.shields.io/travis/vvo/npm-pkgr/master.svg?style=flat-square)](https://travis-ci.org/vvo/npm-pkgr)
[![Dependency Status](http://img.shields.io/david/vvo/npm-pkgr.svg?style=flat-square)](https://david-dm.org/vvo/npm-pkgr)
[![devDependency Status](http://img.shields.io/david/dev/vvo/npm-pkgr.svg?style=flat-square)](https://david-dm.org/vvo/npm-pkgr#info=devDependencies)

npm-pkgr caches `npm install` results by hashing dependencies from `package.json`
and `npm-shrinkwrap.json`.

If your `package.json` did not change from last build, then you will immediately get
either:
- a symlink `node_modules`..
- a full `node_modules` copy..

.. to the latest build result.

npm-pkgr frees your CI server from npm dependency and will make your builds or
deploys run fast.

## Usage

```shell
npm install -g npm-pkgr
```

Use `npm-pkgr` instead of `npm install` and you are done.

```shell
npm-pkgr
```

Hashes and find the latest build corresponding to `package.json` and `npm-shrinkwrap.json`.

```shell
npm-pkgr --production
```

Hashes and fin the latest build corresponding to `npm-shrinkwrap.json`.

### strategy

Default strategy is to symlink `$CWD/node_modules -> ~/.npm-pkgr/$hash/node_modules`.

You can also get a full copy of the `~/.npm-pkgr/$hash/node_modules`.

```shell
npm-pkgr --strategy=copy
```

Carefull, if you `--strategy copy`, you will end up installing the `copy package`

## features

* insanely fast `npm install` if already done
* `npm install` once in your CI server, deploy everywhere
* solves shrinkwrap inconsistencies/problems
* solves devDependencies updates even when you use a shrinkwrap
* concurrent builds
* get symlinks or copy to cached `node_modules`
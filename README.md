# HandsomeMod packages feed

## Description

This is the HandsomeMod "handsomefeed" containing build scripts, options and patches for applications, modules and libraries used within HandsomeMod.

## Usage

This repository is intended to be layered on-top of an HandsomeMod buildroot. If you do not have an HandsomeMod buildroot installed, Just Clone HandsomeMod Repository [HandsomeMod Buildroot](https://github.com/HandsomeMod/HandsomeMod).

This feed is enabled by default. To install all its package definitions, run:
```
./scripts/feeds update handsomefeed
./scripts/feeds install -a -p handsomefeed
```

## Warning

The packages in nonfree directory just for testing!

which come form [Lindenis-org](https://github.com/lindenis-org)

All the packages in this repository only tested to work on HandsomeMod!

## License

handsomefeed is licensed under GPL-2.0


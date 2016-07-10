# ChangeLog

## unreleased

* Should work on windows [#24][] [@toy][]
* Rename `ImageOptim::ImagePath` to `ImageOptim::Path` and its method `#format` to `#image_format` [@toy][]
* Ignore empty config files [#133][] [@toy][]
* Use `FileUtils.move` in `ImagePath#replace` to rename file instead of copying on same device, don't preserve mtime and atime [#134][] [@toy][]
* Make `:allow_lossy` an individual option for workers that can use it, so it will be in the list of worker options [#130][] [@toy][]
* Use first 8 characters of sha1 hex for jpegrescan version [#131][] [@toy][]

## v0.22.1 (2016-02-21)

* Fix missing old (1.x) `pngquant` version as it was output to stderr [#123][] [@toy][]
* Fix capturing wrong version of `pngcrush` when it complains about different png.h and png.c [#122][] [@toy][]
* Add support for `sprockets-rails` 3.x, kudos to [@iggant][] and [@valff][] for initial PRs [#120][] [#121][] [#126][] [@toy][]
* Use rubocop ~> 0.37 [@toy][]

## v0.22.0 (2015-11-21)

* Unify getting description of option default value using `default_description` [@toy][]
* Don't use `-strip` option for optipng when the bin version is less than 0.7 [#106][] [@toy][]
* Use quality `0..100` by default in lossy mode of pngquant worker [#77][] [@toy][]
* Add `:disable_plugins` and `:enable_plugins` options to `svgo` worker [#110][] [@tomhughes][]
* Allow setting config in rails like `config.assets.image_optim.name = value` [#111][] [@toy][]

## v0.21.0 (2015-05-30)

* Use exifr 1.2.2 with fix for a bug [#85][] [@toy][]
* Change order of png workers according to analysis to pngcrush, optipng, pngquant, pngout, advpng (was pngquant, pngcrush, pngout, advpng, optipng) [@toy][]
* Run worker command without invoking shell (except ruby < 1.9 and jruby) [@toy][]
* Add disabling worker by passing `:disable => true` (previously only by passing `false` instead of options hash) [@toy][]
* Add tests for railtie, also to prevent [issues like #72](https://github.com/toy/image_optim/issues/72) [#73][] [@toy][]
* Remove haml development dependency [@toy][]
* Add `-strip` option to optipng worker to remove all metadata chunks, on by default [#75][] [@jwidderich][]
* Fixing minor spelling mistakes from `--help` output [#79][] [@kaspergrubbe][]

## v0.20.2 (2014-12-26)

* Fix `ImagePath#temp_path` for ruby 2.2 caused by `Tmpname#make_tmpname` accepting only objects directly convertible to String for prefix and suffix starting with 2.2 [#74][] [@toy][]

## v0.20.1 (2014-12-19)

* Fix [paperclip-optimizer issue #13](https://github.com/janfoeh/paperclip-optimizer/issues/13): railtie broken with `undefined local variable or method 'app'` [#72][] [@janfoeh][]

## v0.20.0 (2014-12-15)

* Ignore and show warning for lossy options `jpegoptim#max_quality` and `pngquant#quality` in default/lossless mode [#71][] [@toy][]
* Add `:blacken` option to `pngcrush` worker, to blacken fully transparent pixels, on by default [@toy][]
* Command line option `--no-progress` to disable showing progress of optimizing images [@toy][]

## v0.19.1 (2014-11-22)

* Blacklist pngcrush 1.7.80 as it loses one color in indexed images [@toy][]

## v0.19.0 (2014-11-08)

* Added lossy worker `jpegrecompress` (uses [`jpeg-recompress`](https://github.com/danielgtaylor/jpeg-archive#jpeg-recompress)), disabled unless `:allow_lossy` is true [#65][] [@wjordan][] [@toy][]
* `:allow_lossy` option to allow lossy workers and optimizations [@toy][]
* Don't warn multiple times about problematic binary [#69][] [@toy][]
* Run gisicle two times (with interlace off then with on) if interlace is not set explicitly [#70][] [@toy][]
* Remove app and other extensions from gif images [@toy][]
* Change behaviour of gifsicle interlace option to deinterlace for `false`, pass `nil` to leave as is [@toy][]
* Worker can change its initialization by overriding `init` and can initialize multiple instances [#70][] [@toy][]

## v0.18.0 (2014-11-01)

* Add interface to `image_optim_pack` [@toy][]
* Use `in_threads ~> 1.3` [@toy][]
* Added options to Gifsicle, specifically --careful (for compatibility) and --optimize for granularity [#51][] [@kaspergrubbe][]
* `:skip_missing_workers` option to skip workers with missing or problematic binaries [#66][] [@toy][]
* Speedup specs (~8x) [#60][] [@toy][]
* `script/worker_analysis` to compare worker chains by optimization, time and losslessness [@toy][]
* `Cmd` module to ensure interrupted commands can't go unnoticed [@toy][]

## v0.17.1 (2014-10-06)

* Fix bin path resolving method missing vendor directory [@toy][]

## v0.17.0 (2014-10-04)

* Use pure ruby detection of bin path [@toy][]
* Fail if version of bin can't be detected [#39][] [@toy][]
* Check path in `XXX_BIN` to exist, be a file and be executable [@toy][]
* `image_optim --info` to perform initialization with verbose output without running optimizations [@toy][]
* Changeable config paths [@toy][]

## v0.16.0 (2014-09-12)

* Wrote this ChangeLog [#62][] [@toy][]
* Use rubocop ~> 0.26.0 [@toy][]
* Install advancecomp from source in travis script [#61][] [@toy][]
* Move expansion of config path to read method and rescue with warning [#58][] [@toy][]
* Show workers options in verbose mode [#56][] [@toy][]
* Resolve all bins during initialization [#22][] [@toy][]
* Add exclusion glob patterns, `.*` by default [#35][] [#48][] [@toy][]
* Show better warning when running image_optim for a directory without recursive option [@toy][]
* Use stable sort for workers [@toy][]
* Check binary version instead of using which to check if binary is present [#59][] [@toy][]

## v0.15.0 (2014-08-19)

* Use advpng worker before optipng [@toy][]
* Fix order of results (use progress ~> 3.0.1) [@toy][]
* Change array returned from `optimize_images`, `optimize_images!` and `optimize_images_data` to contain pairs of item and result instead of just result [@toy][]
* Fixed `Space` causing exception with negative numbers [@toy][]
* Added pngquant worker [#14][] [#32][] [#40][] [#52][] [@adammathys][] [@smasry][] [@toy][]
* Add instructions to errors from bin resolver [@toy][]
* Use in_threads ~> 1.2.2 with fix for silent exceptions [@toy][]
* Fix `LocalJumpError` in railtie initializer block (ruby 2.1.2, rails 4.1.4) [#50][] [@schnittchen][]

## v0.14.0 (2014-07-17)

* Added Inch CI and Gittip badges to README [@toy][]
* Assign worker options to constants for documentation [@toy][]
* Code style, reorganized, comments, added rubocop [@toy][]
* Switch to rspec 3.0 [@toy][]
* Don't mention versions in instructions for installing jpegoptim and pngcrush [@toy][]

## v0.13.3 (2014-05-22)

* Added instruction about libjpeg-turbo-utils [#49][] [@toy][]

## v0.13.2 (2014-04-24)

* Updated versions of `pngcrush` and `jpegoptim` in installation instructions [#46][] [@toy][]
* Script for updating instructions in README [@toy][]
* Typo in README [#45][] [@rawsyntax][]

## v0.13.1 (2014-04-08)

* Use image_size ~> 1.3.0 so only `FormatError` exceptions are caught and show warning [#44][] [@lencioni][]

## v0.13.0 (2014-04-06)

* Detect and warn about broken images [#43][] [@toy][]
* Output image_optim version when running in verbose mode [@toy][]
* Show resolved version in version exceptions and warnings [@toy][]
* Warn if advpng version is less than 1.17 as it does not use zopfli [#17][] [#18][] [@toy][]

## v0.12.1 (2014-03-10)

* Don't try to register preprocessors when sprockets library is not initialized (app.assets is nil) [#41][] [@toy][]
* Output resolved binaries when verbose [@toy][]
* Output nice level and number of threads when verbose [@toy][]
* Output config to stderr when verbose [@toy][]
* Don't limit number of threads [@toy][]

## v0.12.0 (2014-03-02)

* Checking bin versions [#33][] [@toy][]

## v0.11.2 (2014-03-01)

* Fixed building PATH environment variable [@toy][]

## v0.11.1 (2014-02-20)

* Allow `-v` for version if it is the only argument [@toy][]
* Fixed initializing railtie [#37][] [@toy][]

## v0.11.0 (2014-02-16)

* Use image_size ~> 1.2.0 [@toy][]
* Added `svgo` worker and support for svg files [#27][] [#30][] [@nybblr][]
* Properly unlink temporary files [#29][] [@toy][]
* Read options from rails app configuration `app.config.assets.image_optim` in railtie [#31][] [@bencrouse][]
* Updated versions of `pngcrush` and `jpegoptim` in installation instructions [#26][] [@jc00ke][]

## v0.10.2 (2014-01-25)

* Fixed regression with progress introduced in v0.10.0 [@toy][]

## v0.10.1 (2014-01-23)

* Ensure binary data (ruby 1.9+) from `optimize_image_data` and `optimize_images_data` [#25][] [@toy][]
* Mention `optimize_image_data` and `optimize_images_data` in README [#25][] [@toy][]

## v0.10.0 (2013-12-25)

* Fixed bug with inheritance of `DelegateClass` in jruby 1.9 and 2.0 [@toy][]
* Return `ImagePath::Optimized` containing also original path and size from `optimize_image` and `optimize_image!` [#12][] [@toy][]
* Show exception backtrace when verbose [@toy][]
* Fail if there were warnings with paths to optimize [@toy][]
* Rails (sprockets) preprocessor [#2][] [@toy][]
* Use fspath ~> 2.1.0 with fixes for jruby 1.7.8 [@toy][]
* Add `optimize_image_data` and `optimize_images_data` [@toy][]
* Read config from `image_optim.yml` at `XDG_CONFIG_HOME` (`~/.config` by default) and from `.image_optim.yml` in current working directory [#13][] [@toy][]
* Added badges to README [@toy][]
* Big refactoring [@toy][]

## v0.9.1 (2013-08-20)

* Use progress ~> 3.0.0 and in_threads ~> 1.2.0 [@toy][]

## v0.9.0 (2013-07-30)

* Use fspath ~> 2.0.5 with bug fix for jruby in 1.8 mode [@toy][]
* Overcome wrong implementation of `Process::Status` in jruby [@toy][]
* Fix for jruby not `File.rename` not accepting non String [@toy][]
* Fix for jruby `File.rename` not accepting non String [@toy][]
* Added `.travis.yml` [@toy][]
* Added `jhead` worker [@toy][]

## v0.8.1 (2013-05-27)

* Fixed variable name in `jpegoptim` worker [@toy][]
* Added example of using `PATH` with ImageOptim.app bins [#11][] [@toy][]

## v0.8.0 (2013-03-27)

* Print options if verbose [@toy][]
* Added worker options to README using script [#5][] [@toy][]
* Setting worker options using arguments to image_optim bin [@toy][]
* Option definitions with description, default value and validation instead of attribute reader in options [@toy][]
* Don't change PATH for ruby process [@toy][]
* Vendor `jpegrescan` [@toy][]
* Option to use `jpegrescan` in `jpegtran` worker, off by default [#6][] [@toy][]

## v0.7.3 (2013-02-24)

* Use image_size ~> 1.1.2 [@toy][]

## v0.7.2 (2013-01-18)

* Make `apply_threading` accept enum instead of array [@toy][]

## v0.7.1 (2013-01-17)

* Use more compatible redirect syntax `>&` [#9][] @"Chris Thompson"

## v0.7.0 (2013-01-17)

* Use `system` with `env` and `nice` instead of forking [#8][] [@toy][]
* Don't use `-s` of `which` as it is nonstandard [#7][] [@toy][]
* Added bin resolving with ability to specify binary paths using environment variables [@toy][]
* Reorganized workers [@toy][]
* Added links to tool projects [@toy][]

## v0.6.0 (2012-11-15)

* Warn if directly added files are not images or are not optimizable [@toy][]
* Recursively scan directories for images [#4][] [@toy][]
* Typo in bin/image_optim  [#3][] [@fabiomcosta][]

## v0.5.1 (2012-08-07)

* Nice output for configuration and binary resolving errors [@toy][]

## v0.5.0 (2012-08-05)

* Verbose output [@toy][]

## v0.4.2 (2012-02-26)

* Use image_size ~> 1.1 [@toy][]

## v0.4.1 (2012-02-14)

* Added binary installation instructions to README [#1][] [@jingoro][]

## v0.4.0 (2012-01-13)

* Added usage to README [@toy][]
* Allow setting nice level, 10 by default [@toy][]
* Use `fork` instead of `system` [@toy][]

## v0.3.2 (2012-01-12)

* Fixed setting max thread count [@toy][]

## v0.3.1 (2012-01-12)

* Fixed parsing thread option [@toy][]

## v0.3.0 (2012-01-12)

* Output size change per file and total [@toy][]
* Warn about non files [@toy][]

## v0.2.1 (2012-01-11)

* Simplified determining presence of bin [@toy][]

## v0.2.0 (2012-01-10)

* Reduce number of created temp files to minimum [@toy][]
* Use fspath ~> 2.0.3 [@toy][]

## v0.1.0 (2012-01-09)

* Initial release [@toy][]

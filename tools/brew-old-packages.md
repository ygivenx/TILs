# Install old version using Homebrew

The example follows installation of R package.

The current version on homebrew is 4.3.1.
Need to install version 4.2.2

1. Create a local tap

```bash
brew tap-new $USER/local-R
```

2. Extract the required version from homebrew

```bash
brew extract --version=4.2.2 R rsingh/local-R
```

3. Install the required version

```bash
brew install R@4.2.2
```

# Enjoy App

This is a Electron App.

```bash
yarn install
yarn start
```

需要使用Python 3.11.0
使用pyenv 建立单独的Python环境
```bash
pyenv install 3.11.0
pyenv local 3.11.0
python -m venv .venv3_11
source .venv3_11/bin/activate
```

禁止沙盒
```bash
export ELECTRON_DISABLE_SANDBOX=false

```

然后使用上的`yarn start`构建应用。

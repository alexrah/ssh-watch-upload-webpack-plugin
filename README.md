# SSH Watch Upload Webpack Plugin

A plugin that watches your files and uploads the newly compiled assets to an external server via SSH

## Install

```bash
npm i @alexrah/ssh-watch-upload-webpack-plugin
```

```bash
yarn add --dev @alexrah/ssh-watch-upload-webpack-plugin
```

## Usage

The plugin will hook into Webpack and upload emitted assets to a destination server using a basic SSH connection. Add the plugin to your Webpack config like this:

**webpack.config.js**

```js
const SSHWatchUploadWebpackPlugin = require('ssh-watch-upload-webpack-plugin');

module.exports = {
  entry: ...,
  output: ...,
  plugins: [
    ...,
    new SSHWatchUploadWebpackPlugin({
      mode: ...,
      host: ...,
      port: ...,
      username: ...,
      passphrase: ...,
      privateKey: ...,
      uploadPath: ...,
      domain: ...,
      openDomain: ...,
    }),
  ],
};
```

Once configured, you can run Webpack in watch mode to activate the plugin:

```bash
npx webpack -w
```

```bash
yarn webpack -w
```

Alternatively, you can enable watch mode via the Webpack config:

**webpack.config.js**

```js
module.exports = {
  entry: ...,
  output: ...,
  watch: true, // Enable watch mode
  plugins: [
    ...,
    new SSHWatchUploadWebpackPlugin({...}),
  ],
};
```

When activated you will see the terminal generating logs:

```bash
[SSHWatchUpload] [22:01:48] Connected to server
[SSHWatchUpload] [22:01:49] Watching for changes...
```

After editing and saving a file while in watch mode you will see upload confirmation logs:

```bash
[SSHWatchUpload] [22:30:57] Uploading main.js...
[SSHWatchUpload] [22:30:57] Upload complete: main.js
```

## Options

You can pass a hash of configuration options to `ssh-watch-upload-webpack-plugin`.
Allowed values are as follows:
|Name|Type|Default|Description|
|:--:|:--:|:-----:|:----------|
|**mode**|String|''|Webpack build mode (production \| development)|
|**host**|String|''|External server SSH domain|
|**port**|Number|null|Port used to connect to the external server|
|**username**|String|''|Username used to connect to the external server|
|**passphrase**|String|''|Passphrase used to connect to the external server|
|**privateKey**|String|''|File path of the SHH private key file|
|**uploadPath**|String|''|Path on the external server where files should be uploaded|
|**domain**|String|''|Public facing domain of the server|
|**openDomain**|Boolean|false|Flag to enable the browser to automatically open the domain once connected|

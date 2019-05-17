## NPM - Node Package Manager
npm is world's largest software registry. Open source developers from every continent use npm to share & borrow 
packages, and many organizations use npm to manage private development as well.

**It consists of 3 different things**
* website - use website to discover packages
* command line interface - use this to run commands
* registry - large public database of javascript software & metadata around it

**List of various npm commands** -
1. npm init - creates a package.json file
2. npm create-react-app - creates a new react app
3. npm install, it installs all the dependencies as mentioned in package.json
4. npm install overalys, it will install overlays dependency in your project.
5. npm install overalys --save, it will install overlays also add it in your package.json
6. npm publish to publish a package

**yarn v/s npm**
1. yarn is faster then npm, because npm installs the dependencies sequentially, while yarn installs them parallely.
2. yarn updates yarn.lock file that ensures that exact same package gets installed on every device. These lock files
	actually locks the dependencies to specific versions. While in npm, same thing was acheived using shrinkwrap 
	command, however this doesn't get generated automatically & requires maintenance.
3. yarn caches every package it downloads, so it never downloads again.
4. yarn uses checksum to verify integrity of every installed package before its code is executed.

## Webpack
webpack is a static module bundler for modern javascript applications. When webpack processes the application, it
	internally builds a dependency graph which maps every module your project needs. 

webpack.config.js lets you specify the configuration you can use for customizing the behaviour.

**Some core configurations in webpack.config.js are below -**
* Entry - indicates which module webpack should use to begin building out its internal dependency graph, default
	value for this is ./src/index.js.
	```
		module.exports = {
			entry: './path/to/my/entry/file.js'
		}
	```
* Output - indicates webpack where to emit the bundles it creates & how to name those files. BY default it will 
	output in dist directory.
	```
		module.exports = {
			output: {
				path: path.resolve(__dirname, 'dist'),
				filename: 'main.js'
			}
		}
	```
* Loaders - webpack only understands .js & json files. Loader allow webpack to process other types of files &
	convert them to valid modules that can be consumed by your application & added to dependency graph.
	Ex: you may have .jpg, .png, .css, .scss in your application, how would webpack process them is by using
	loaders
	```
		module.exports = [
			{
				test: /\.css$/,
				use: [
					styleLoader,
					cssLoader
				]
			},
			{
				test: /\.(jpg|png|svg)$/,
				use: [
					urlLoader
				]
			},
		]
	```
* Plugins - can be leveraged to perform a tasks like build optimization, asset management & injection of environment
	variables. There are many plugins available. 1 out of them is DefinePlugin which lets you set environment
	variables at compile time.

When you run - 'npm run build' command does nothing unless you specify what build does in your package.json file.
	It lets you perform any necessary tasks for your project, prior to it being used in other project.

So if you want to run webpack commands to build your output, you can do so in your package.json specifying that 
	in your build command.
Ex: node 'webpack-dir/bin/webpack' --config webpack.config.js(where you can specify all the required options for 
	webpack)
If you have configured that you want source map, webpack generates source maps also for you. 

**What is source map?**
When your source code has gone through transformations, debugging becomes a problem. When debugging in a browser,
how to tell where the original code is? Source maps solve this problem by providing a mapping b/w original & 
transformed source code. 

You can do so by setting devtool as 'source-map' in webpack config. It generates .map file in dist folder for this.

**UglifyJs** is a javascript parser, minifier, compressor & beautifier toolkit. This can take multiple input files & 
then pass options. So this creates minified file.

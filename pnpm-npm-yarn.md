## Comparing NPM, YARN, and PNPM

Package Managers: Which One is Right for Project

##  NPM
Node Package Manager:  NPM has a simple and intuitive command-line interface that allows you to install, update, uninstall, and publish packages. It also has a website (npmjs.com) where you can browse, search, and download packages. NPM uses a file called package.json to store the metadata of your project, such as name, version, dependencies, scripts, etc. It also creates a folder called node_modules where it stores the installed packages.

## `Advantages`

 - It is widely used and supported by the JavaScript community
- It has a large and diverse collection of packages for almost any use case
- It has a rich set of features and options to customize your project
- It has a built-in security audit tool that checks for vulnerabilities in your dependencies
 
## `Disadvantages`
- It can be slow and inefficient when installing or updating packages
- It can create duplicate or nested dependencies that take up disk space and cause conflicts
- It can have inconsistent or outdated versions of packages across different environments

## 

##  YARN
Yet Another Resource Negotiator: YARN has a similar command-line interface as NPM, but with some differences and improvements. It also uses the same package.json file as NPM, but it adds another file called yarn.lock that locks the exact versions of your dependencies. It also creates a node_modules folder where it stores the installed packages.

## `Advantages`

 - It is faster and more efficient than NPM when installing or updating packages
- It uses a flat dependency structure that avoids duplication and nesting of packages
- It supports offline installation of packages from a local cache
- It has a better resolution algorithm that ensures consistent and deterministic versions of packages across different environments
 
## `Disadvantages`
- It is not as widely used or supported as NPM by the JavaScript community
- It may not be compatible with some NPM packages or features
- It may have some bugs or issues that are not yet fixed or resolved

## 

##  PNPM
 Performant Node Package Manager: PNPM has a similar command-line interface as NPM and YARN, but with some differences and enhancements. It also uses the same package.json file as NPM and YARN, but it adds another file called pnpm-lock.yaml that locks the exact versions of your dependencies. It also creates a node_modules folder where it stores the installed packages.

## `Advantages`

 - It is faster and lighter than both NPM and YARN when installing or updating packages
- It uses hard links or symlinks to link packages from a global store instead of copying them to the node_modules folder
- It supports strict dependency isolation that prevents packages from accessing modules that are not declared in their package.json file
- It has a built-in security audit tool that checks for vulnerabilities in your dependencies
 
## `Disadvantages`
- It is not as widely used or supported as NPM or YARN by the JavaScript community
- It may not be compatible with some NPM or YARN packages or features
- It may have some bugs or issues that are not yet fixed or resolved

## 

## Features
This feature allows you to manage multiple sub-projects within a single repository, and share dependencies between them. This is useful for monorepo architectures, where you have multiple packages that depend on each other

## 

## Performance

| Metric                         | NPM    | YARN   | PNPM  |
| ------------------------------ | ------ | ------ | ----- |
| Installation time (cold cache) | 67.4s  | 47.6s  | 32.3s |
| Installation time (warm cache) | 9.1s   | 4.9s   | 4.4s  |
| Disk space used                | 237 MB | 175 MB | 39 MB |

PNPM is the fastest package manager, followed by YARN and then NPM.
 This is because PNPM uses a novel approach called `symlinked node_modules, which creates hard links to the global store of packages instead of copying them to each project`. This saves disk space and reduces duplication. YARN also uses a global cache of packages, but it still copies them to each project. NPM does not use any caching mechanism, so it downloads and installs each package every time.

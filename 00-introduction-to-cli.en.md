# Introduction to CF CLI

## Clone the lab content

```bash
git clone https://github.com/kathywan/PCF-CN-Workshop-BR
```

- Change the working directory to be _PCF-CN-Workshop-BR/labs_

## How to target a foundation and login

*PWS*

* Open a Terminal (e.g., `cmd` or `bash` shell)

* Target a foundation and login

```bash
cf api https://api.run.pivotal.io --skip-ssl-validation
cf login
```
* Enter your account username and password, then select an org and space.

Alternatively, you can target explicitly:

```bash
cf target -o myorg -s myspace
```

## How to deploy an application

* Let's take a look at the CF CLI options
```bash
  cf help -a
```
* Let's see what buildpacks are available to us
```bash
  cf buildpacks
```
* Peruse the services you can provision and bind your applications to

```bash
  cf marketplace
```
* Time to deploy an app. How about Node.js?

```bash
  cd nodejs-cf-sample-app
  cf push
```

* Check what applications have been deployed so far
```bash
  cf apps
```
Take some time to visit each of the applications you've just deployed.

* Let's stop an app, then check that it has indeed been stopped

```bash
  cf stop cf-nodejs
  cf apps
```

## How to cleanup after yourself

* Finally, let's delete an app
```bash
  cf delete cf-nodejs
```

## Where to go for more help

[Getting Started with the CF CLI](https://docs.cloudfoundry.org/cf-cli/getting-started.html)

[Cloud Foundry CLI Reference Guide](http://cli.cloudfoundry.org/en-US/cf/)

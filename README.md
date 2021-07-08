![Aeroplan Hero Logo](https://www.aircanada.com/content/dam/aircanada/loyalty-content/images/hero-aeroplan.png)
# AC Loyalty Dashboard UI project

Welcome to Air Canada's Loyalty Dashboard Team!

This document is meant to help new developers to quickly get up and running in a straight forward fashion. Please review the below documentation before getting started. We promise it's not that long.

If you are new to the project, require a walkthrough, or are confused please reach out to any of the below leads for help,

>> We are currently seeking feedback on this README upgrade, please let any of the leads know if you have any feedback, suggestions, or if we are missing an important section.

Pod | Lead | ...
--- | ---- | ---
2 | Tahsin Mostafiz | ...
3 | Basil Earle | ...
6 | David Leung | ...

Other README articles available,
- [Application Architecture](./readmes/application-architecture.md)
- [Environments](./readmes/environments.md)
- [Helpful Links and Artlices](./readmes/helpful-links.md)  

## Dependencies

**Please ensure that your development machine has the below dependencies installed before running or working with this project**

* Yarn (> 1.0.0 < 2.0.0)
* Node (> 12)

## Commands 

### Download dependencies

This command will download all `node_modules` required for the project, it is good to run this command from time to time to ensure your development machine is up to date with all the latest modules

*If your application is throwing errors stating something along the lines of `not found` please run this command to first see if your modules are out of date*

```
  yarn --check-files
```

*the `--check-files` flag ensures the command does a deep check to ensure that all modules imported by the embedded modules are up to date as well*

### Run in Development Mode

This command will run the angular builder and deploy the code live using webpack's dev server plugin

This command uses the environment files located at the root of the `environment/` folder 

```
  yarn start
```

*to point your local development environment to a different environment, you can copy and paste the files of a the `environment/*` folder, to the root of `environment`.*

### Creating a deployment artifact locally
```
  yarn build:prod

  # OR, if you want to specify a particular environment for test

  yarn build:prod -c dev|int|uat|bat|pre-prod|production
```

to run this generated artifact, you will need a some form of application server running, with routing fallback enabled. This can easily be done with nginx, or the NPM angular-http-serve module.

**IMPORTANT** If you choose to run the generated artifacts with an angular-http-serve like library, ensure to comment out the GZIP step in `config/extra-webpack-config.js`, otherwise the served assets will not be able to be understood by the browser.

## Creating new Components / Stores / Services, etc.

**PLEASE DO NOT USE THE ANGULAR CLI COMMANDS**

Since this project leverages the Amadeus Otter library, we use different commands to create new modules and files, instead of the typical `ng` commands.

### New Components

*to learn more about the container / presenter strategy, please refer to the helpful links document*

The below command will generate a new component within our `src/components` folder. You will have the option to generate a containter, presenter or both

```
  yarn generate:component
```

Option | Default | Description
------ | ------- | -----------
name | <no default value> | whatever you would like to name your component, define in lowerCamelCase
structure | full / container / presenter | select based off your needs
fixtures | No | creates fixtures files for certain test case scenarios, these are not required. Please select `No`
theming | No | we do not use Otter theming, please select `No`
description | <no default value> | whatever description you can give to your component to help others better understand what its for
analytics | No | We do not use Otter analytics, **DO NOT CONFUSE WITH AC ANALYTICS** we do not use this, please select `No`
dummy | No | Generates a lot of boilerplate we do not require, please select `No`

As a post clean up task, please ensure to remove any `*.context.ts` files, as they are not required for our project, and are generated automatically

### New Services

The below command will generate a new service within our `src/services` folder

```
  yarn generate:service
```

When working with services, please be smart with how you leverage them, or include them in the project. Your service can be imported through root and always be available (like the confetti service, or breakpoints service), or you can import it via an Angular module if they will only be used in specific pages or components in the application.

Option | Default | Description
------ | ------- | -----------
name | <no default value> | whatever you would like to name your service, define in lowerCamelCase
feature | base | a nested folder within your service structure, typically we leave it to the default value of `base`

### New Stores/Store Entries

The below command will generate a new service within our `src/store` folder

```
  yarn generate:store
```

Similar to services, please be smart when deciding where to import your store module. Unlike services or components, once a store module is imported it becomes available to any component or page thereafter, so import it at the first instance it's required.

Option | Default | Description
------ | ------- | -----------
type | simple-async or simple-sync | this tells the generator whether or not to auto generate async actions and effect files for your store. We do not use entities, please do not select one of those options
name | <no default value> | whatever you would like to name your store, define in lowerCamelCase
sdk | **leave empty** | we do not use the `@dapi/sdk`'s so just leave this blank
sdk model | **leave empty** | we do not use the `@dapi/sdk`'s so just leave this blank

### New Pages

The below command will generate a new page within our `src/app/pages` folder

```
  yarn generate:page
```

*Based on the flow your working on, you may need to move the page you generated, into one of the parent page folders*

Option | Default | Description
------ | ------- | -----------
name | <no default value> | whatever you would like to name your service, define in lowerCamelCase
scope | **leave empty** | we do not use the `@dapi/sdk`'s so just leave this blank
feature | app-routing | we use a different routing strategy that what otter provides by default, just use the default value
# air_canada

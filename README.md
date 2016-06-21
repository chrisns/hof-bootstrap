# Home Office Forms Bootstrap

Home Office Forms (HOF) Bootstrap is a highly configurable mechanism for creating and optionally, launching your service.

## Bootstrap is a function

You can call the `bootstrap` function with a list of [routes](#routes) and your [custom settings](#custom-settings) to invoke your personally configured service.

```
const bootstrap = require('hof-bootstrap');

bootstrap({
  views: ...,
  errorHandler: ...,
  ...,
  routes: [{ ... }, { ... }]
});
```

**NOTE**: `bootstrap` returns a promise that resolves with with the bootstrap interface, which means you can call methods on bootstrap, such as;
```
bootstrap({ ... }).then(bootstrapInterface => {
  if (conditionIsMet)
    bootstrapInterface.stop();
    bootstrapInterface.use(middleware);
    bootstrapInterface.start();
  }
});
```

## Options

- `assets`: Location of the static assets are served relative to the root of your project. Defaults to 'public'.
- `views`: Location of the base views relative to the root of your project. Defaults to 'views'.
- `fields`: Location of the common fields relative to the root of your project. Defaults to 'fields'.
- `translations`: Location of the common translations relative to the root of your project. Defaults to 'translations'.
- `viewEngine`: Name of the express viewEngine. Defaults to 'html'.
- `start`: Start the server listening when the bootstrap function is called. Defaults to `true`.
- `getCookies`: Load 'cookies' view at `GET /cookies`.
- `getTerms`: Load 'terms' view at `GET /terms-and-conditions`.
- `errorHandler`: Error handling middleware. Defaults to `hof.middleware.errors`.


## Routes

The most important element of your service are the routes. These are what you will use to define the path your user will take when completing your forms.

### Settings
Not all route settings are mandatory, you can create and launch a service with just a set of steps.

#### Required
- `steps`: An object that defines the url, fields and optionally more for each form within your service.

For example, the following step will validate two fields. When submitted, if both fields are successfully validated, the next step to be loaded will be '/two'.
```
steps: {
  '/one': {
    fields: [
      'name_of_field_one',
      'name_of_field_two'
    ],
    next: '/two',
    forks: [{
      target: '/three',
      field: 'option1',
      value: 'yes'
    }]
  }
}
```
[Read more about steps and fields](UkHomeOffice/hof/documentation)

#### Options
- `baseUrl`: Base url from which all steps are relative. Defaults to `/`.
- `fields`: Location of the routes' fields, relative to the root of your project. Defaults `fields`.
- `views`: Location of the routes' views relative to the root of your project. Defaults `views`.


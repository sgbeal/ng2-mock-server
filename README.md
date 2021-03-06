ng2-mock-server
===============

An angular2 mock XHRBackend to ease front-end development when no real back-end is available.

- No need to run a back-end on the dev machine.
- Easy to show off a front-end from static servers like GitHub Pages, etc.
- Easy to implement back-end functionality that runs in the browser. When the back-end is ready, just remove it and it's using the back-end with no changes in your application code.

Getting started
---------------

    npm install ng2-mock-server [--save | --save-dev]

In your `bootstrap.ts` or `main.ts` file:

    import {Http} from 'angular2/http';
    import {MOCK_SERVER_PROVIDERS, MockSrvRouter} from 'ng2-mock-server/http';

    // This is where you implement the mock back-end logic:
    import {setupMockRouter} from './src/setupMockRouter';

    bootstrap([
        // your normal providers
        Http,
        MOCK_SERVER_PROVIDERS,
    ], AppComponent).then(app => {
        let router = <MockSrvRouter> app.injector.get(MockSrvRouter);

        setupMockRouter(router);
    });

In `./src/setupMockRouter.ts`:

    export function setupMockRouter(r : MockSrvRouter) {
        r.get("/hello", (req : Request, ...params : string) {
           return res(200, "world");
        });

        r.get("/hello/:name", (req : Request, name : string) {
            return res(200, name);
        });

        // Important, tell the router you're done setting up routes.
        r.ready();
    }

Contributions
-------------

Please create issues with bug reports, feature requests or asking for help.

Pull requests more than welcome.

Licence
-------

Released under the MIT Licence.

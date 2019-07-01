## Overview

This project uses [Express.js](https://expressjs.com/) to statically serve a pre-rendered [React Application](https://github.com/facebook/create-react-app), this is then hydrated by React to allow usage.

This allows:

- Faster rendering
- Traditional SEO performance

## Resources

- [ReactDOMServer](https://reactjs.org/docs/react-dom-server.html)
- [Express Documentation](https://expressjs.com/)

## Notes

### React Application

Everything within the `/src` dir is a traditional React application, care would have to be taken to ensure no explicit reliance on global variables etc. within here otherwise we could cause issues.

For example an application with a Component which bases its output on screen height would fail when rendering via an express server that _has no screen_.

### Express Application

The express application is essentially just the `server.js` file in the root. It does several things very simply:

- Imports `React`/`ReactDOMServer` as well as our root `App` component
- Replaces the build `index.html` #root element with a clone containing a pre-rendered version of our application
- Uses the express router to capture any connection and return this static application
- Whitelists the build directory so that the application can access it's own files when attempting to do... everything!
- Listens on a specified port for all of the above

## Run Application

To run the application:

1. Clone the repo `git clone https://github.com/jmcgrory/ssr-example.git`
2. Install dependencies `npm install`
3. Build application and serve via `npm build`
4. View application on port specified in terminal output

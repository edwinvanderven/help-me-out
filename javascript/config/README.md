# Info

Having a configuration file inside an application can be useful for environment specific settings. This setup is a lot like having a `.env.*` file but because it is in JavaScript it can give more flexibility.

```javascript
// config.js

const configLookup = {
  localhost: localConfig,
  "develop-host": devConfig,
  "test-host": testConfig,
  "production-host": prodConfig,
};

const getConfig = () => {
  const hostname = window.location.hostname || "";
  return configLookup[hostname] || prodConfig;
};
```

The individual `*Config` files can hold things like feature flags,

```javascript
// config.js
// devConfig = { featureFlags: { ... } }

export const getFlag = (type) => {
  const flags = getConfig().featureFlags;
  if (flags[type]) {
    return true;
  }
  if (localStorage.getItem(`${PREFIX}${type}`) === "true") {
    return true;
  }
  return false;
};
```

The useful thing here is that an individual can add the flag to the localStorage and quickly check if it works as expected.

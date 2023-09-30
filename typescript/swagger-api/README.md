A small NodeJS script that fetches the `openapi.json` data and converts it into TypeScript.

```javascript
const fs = require("fs");
const path = require("path");

const { generateApi } = require("swagger-typescript-api");

const SwaggerMappings = {
  TestService: "<insert url to json file here>/openapi.json",
};

const main = async () => {
  for (const serviceName in SwaggerMappings) {
    const url = SwaggerMappings[serviceName];
    try {
      const { files } = await generateApi({
        name: `${serviceName}.ts`,
        output: path.resolve(process.cwd(), "./src/apis/services"),
        url,
      });
      files.forEach(({ content, name }) => {
        fs.writeFileSync(
          path.resolve(process.cwd(), `./src/apis/services/${serviceName}.ts`),
          content
        );
      });
    } catch (e) {
      console.error(e);
    }
  }
};

main();
```

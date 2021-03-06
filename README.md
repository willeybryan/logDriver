# CDS Log Driver 🇨🇦

Log driving is a means of moving logs (sawn tree trunks) from a forest to sawmills and pulp mills downstream using the current of a river.

In our case we want to move logs (console messages) out of developer consoles and into places like StackDriver.

[![Phase](https://img.shields.io/badge/Phase-Beta-22a7f0.svg)](https://digital.canada.ca/products/)  [![Maintainability](https://api.codeclimate.com/v1/badges/f3fbbbb66e6823d680c6/maintainability)](https://codeclimate.com/github/cds-snc/logDriver/maintainability)

Creates a standardized logging format for output + log collection.

```javascript
standardPayload = {
  cloudEventsVersion: "0.2",
  contentType: "text/plain",
  data: msg,
  eventID: uuidv4(),
  eventTime: new Date().toISOString(),
  eventType: "com.github.cds-snc." + level,
  eventTypeVersion: "1.0",
  source: "/"
};
```

Install with `yarn add @cdssnc/logdriver` or `npm install @cdssnc/logdriver`.

## Adapters

#### StackDriver Node

Add credentials to you .env file

```bash
GOOGLE_APPLICATION_CREDENTIALS="...67550c60cde8.json"
```

Import the logger into your app

```javascript
import { Logger, StackDriverNode } from "@cdssnc/logger";
Logger.subscribe("error", StackDriverNode.log);
Logger.debug("The message from the server"); //logs to console + StackDriver
```

#### StackDriver Client
```javascript
import { Logger, StackDriverClient } from "@cdssnc/logger";

StackDriverClient.init(
   "your-api-key",
   "your-project-id"
);

// window.onError should now catch and report to StackDriver
Logger.subscribe("error", StackDriverClient.log);
Logger.warn("Client side message sent to StackDriver");
```

### Questions?

Please contact us through any of the multiple ways listed on our [website](https://digital.canada.ca/).

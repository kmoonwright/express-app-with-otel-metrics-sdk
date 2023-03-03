# Hello World Express Example

## Overview

This example illustrates a simple hello world using a local dependency and express.

## Usage

### Install and setup

```bash
npm run setup
```

### Running the main application

```bash
HONEYCOMB_API_KEY="hlytN0XOIfKD6WieCXpikI" OTEL_SERVICE_NAME="hello-node-express" npm start
```

Alternatively, to export telemetry using `gRPC` instead of `http/protobuf`:

```bash
HONEYCOMB_API_KEY={apikey} OTEL_SERVICE_NAME="hello-node-express" OTEL_EXPORTER_OTLP_PROTOCOL=grpc npm start
```

You can now curl the app:

```bash
curl localhost:3000
Hello, World!
```

## Using the OpenTelemetry Metrics SDK
```javascript
  // Create additional runtime metrics to emit telemetry data
  const gauge = meter.createObservableGauge(
    'process.runtime.nodejs.memory.heap.total',
    {
      unit: 'By',
      valueType: ValueType.INT,
    },
  );
  gauge.addCallback((result) => {
    console.log('Getting value of process.memoryUsage().heapTotal');
    result.observe(process.memoryUsage().heapTotal);
  });
```
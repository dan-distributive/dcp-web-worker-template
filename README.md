# DistributiveWorker Template

A **vanilla implementation of a DCP Browser Worker** with full event logging and configuration options. This template provides a starting point for anyone wanting to integrate a DCP worker into any webpage with real-time console output and complete sandbox monitoring.

## Try it
Live interactive JSFiddle: [https://jsfiddle.net/DCP_team/g29or41j/](https://jsfiddle.net/DCP_team/g29or41j/)

## Overview

This repository is designed as a tutorial rather than a production-ready system. The code is intended to be clear and easy to understand, allowing developers to modify it as needed. Many configuration values are hard-coded (worker id, deposit account, compute groups, minimum wage, etc.), but they can and should be adapted or parameterized for more advanced use cases.

If you encounter any issues or have questions, you can reach the team via:

* Email: info@distributive.network
* Slack: [DCP Developers Slack](https://join.slack.com/t/dcp-devs/shared_invite/zt-56v87qj7-fkqZOXFUls8rNzO4mxHaIA)


## Features

- Full DistributiveWorker setup with `identity` and `deposit account` configuration
- Earn `Compute Credits` into your deposit account
- Support for multiple `compute groups`
- Control over `CPU/GPU cores`, `utilization`, and `minimum wage`
- Full logging of `worker events`:
  - Fetching work
  - Sending results
  - Payment events
  - Connection and disconnection
  - Errors and Warnings
  - Worker start/stop/end
- Full logging of `sandbox events`:
  - Ready, job received, slice started/ended
  - Progress updates, metrics (CPU/GPU usage, I/O)
  - Payment events
  - Sandbox termination
- Toggle between starting and stopping the worker
- Lightweight, single HTML file implementation for quick testing or prototyping


## Getting Started

### Prerequisites

- A modern web browser (Chrome, Firefox, Edge, Safari)
- An account on [dcp.cloud](https://dcp.cloud) where Compute Credits will be deposited
- (optional) learn more about Compute Credits and how they work [here](https://docs.google.com/document/d/1F6r6yGfVhRxmYT8YzGpzlXhK1jQhOenjDY7dVCSoL5M/edit?usp=sharing)

### Usage

1. Open `index.html` in your browser.
2. Click the **Work!** button to start the worker.
3. The worker logs all events to the textarea on the page in real-time.
4. Click **Stop!** to halt the worker.
5. Refresh the page if you want to run the worker again


### Configuration Options

#### Worker Identity
```javascript
const id = await new dcp.wallet.Keystore("null", "");  // generates random id
await dcp.identity.set(id);
```

#### Deposit Account
```javascript
paymentAddress: new dcp.wallet.Address("YOUR_DEPOSIT_ACCOUNT"),
```

#### Compute Groups
```javascript
computeGroups: [
  { joinKey: "demo", joinSecret: "dcp" },
],
```

#### Cores and Utilization
```javascript
cores: { cpu: 4, gpu: 1 },
utilization: { cpu: 1, gpu: 1 }
```

#### Sandbox Concurrency
```javascript
maxSandboxes: 4
```

#### Minimum Wage
```javascript
minimumWage: {
  "CPU": <credits per CPU-millisec>,
  "GPU": <credits per GPU-millisec>,
   "in": <credits per ingress byte>,
  "out": <credits per egress byte>,
}
```

#### Job Filtering
```javascript
jobIds: false // Or provide an array of job IDs to exclusively run
```

### Event Logging

The template logs **all important worker and sandbox events** to a textarea console, including:
- `worker.connect` / `worker.disconnect` / `worker.start` / `worker.stop` / `worker.end` – worker lifecycle

- `worker.fetch` – when new job slices are fetched

- `worker.result` – after sending results

- `worker.payment` – payment received

- `worker.error` / `worker.warning` – worker errors and warnings

- `sandbox.ready` / `sandbox.job` / `sandbox.slice` / `sandbox.progress` / `sandbox.metrics` / `sandbox.sliceEnd` / `sandbox.payment`

This provides full visibility into worker activity and sandbox execution.


## Customization

- Modify compute groups, cores, utilization, or minimum wage to match your environment.
- Restrict to specific job IDs if desired.
- Extend logging or integrate with your own UI.

## License

MIT License – feel free to use and modify for your own DCP projects.

## Questions?

Explore the Distributive Compute Platform [documentation](https://docs.dcp.dev) for more details on the Compute, Wallet, and Worker APIs and advanced configurations.

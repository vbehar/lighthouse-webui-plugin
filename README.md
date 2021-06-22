# Lighthouse Web UI

This is a Web UI for [Lighthouse](https://github.com/jenkins-x/lighthouse), to visualize:
- **Webhook events** (push, comments, ...) and the related jobs triggered by each event
- **Lighthouse Jobs**
- **Lighthouse Merge Status** from [Keeper](https://github.com/jenkins-x/lighthouse/tree/main/pkg/keeper)
- **Lighthouse Merge History** from [Keeper](https://github.com/jenkins-x/lighthouse/tree/main/pkg/keeper)

The goal is to make it easy to see what is happening inside Lighthouse.

## Screenshots

![events](docs/screenshots/events.png)

![jobs](docs/screenshots/jobs.png)

![merge-status](docs/screenshots/merge-status.png)

![merge-history](docs/screenshots/merge-history.png)

## How It Works

It is a Lighthouse External Plugin, and as such, it receives all the webhook events. It stores them in a [Bleve](http://blevesearch.com/) index - which can be persisted on disk in a PVC (when deployed in Kubernetes).

It also uses the "informer" Kubernetes pattern to keep a local cache of the Lighthouse Jobs, and index them in an in-memory [Bleve](http://blevesearch.com/) index.

And it periodically sync the Lighthouse Keeper state, by polling the "merge pool" JSON and "merge history" JSON from the Keeper service.

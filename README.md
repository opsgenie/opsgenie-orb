# Opsgenie Orb 

Easily send [CircleCI](https://circleci.com/ "CircleCI") job results to create alert in [Opsgenie](https://www.opsgenie.com/ "Opsgenie"). Opsgenie is a dispatcher for CircleCI build failures; determines the right people to notify based on on-call schedules– notifies via email, text messages (SMS), phone calls and iPhone & Android push notifications, and escalates alerts until the alert is acknowledged or closed. For more information, please visit [Opsgenie doc](https://docs.opsgenie.com/docs/circleci-integration "Opsgenie Doc")
Learn more about [Orbs](https://circleci.com/docs/2.0/using-orbs/ "Using Orbs").

## Usage
Example config:

```yaml
version: 2.1

orbs:
  opsgenie: opsgenie/opsgenie@x.y.z

jobs:
  build:
    docker:
      - image: <docker image>
    - opsgenie/<command>
```

## Commands

### Notify
Send notification to opsgenie for CircleCI builds.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `endpoint` | `env_var_name` | ${OPSGENIE_WEBHOOK} | Use the CircleCI UI to add your token under the 'OPSGENIE_WEBHOOK' env var |
| `on_failure` | `boolean` | `false` | Failure information of circleci build |
| `on_success` | `boolean` | `true` | Success information of circleci build_ |

Example:

```yaml
version: 2.1

orbs:
  opsgenie: opsgenie/opsgenie@x.y.z

jobs:
  build:
    docker:
      - image: <docker image>
    - opsgenie/notify
```

## Dependencies / Requirements

### Bash Shell
Due to the limitations of the `sh` shell, `Bash` is required. `Bash` is the default shell used on CircleCI and the Orb will be compatible with most images. Images such as `Alpine` that do not contain the `Bash` shell by default are incompatible and en error message will be logged. You may install the Bash shell through your package manager (example: `apk add bash`) in the Dockerfile for the image you are using.

### cURL
cURL is used to post the Webhook data and must be installed in the container to function properly.

## Help

### Add CircleCI integration in Opsgenie

1. Please [create an Opsgenie account](https://www.opsgenie.com/#signup) if you haven't done so already.
2. Go to [Opsgenie CircleCI Integration](https://app.opsgenie.com/integration#/add/CircleCI) page.
3. Copy the Url to use in CircleCI configuration. You should save this URL as [Enviroment Variable Name](https://circleci.com/docs/2.0/reusing-config/#environment-variable-name). 
To save URL as Enviroment Varible, In the settings page for your project on CircleCI, click Environment Variables. From that page you can click the Add Variable button. Finally, enter URL that you copied from Opsgenie integration page, and OPSGENIE_WEBHOOK as the name.
4. Click Save Integration.

For more information, please visit [Opsgenie circleci documentation](https://docs.opsgenie.com/docs/circleci-integration)
 
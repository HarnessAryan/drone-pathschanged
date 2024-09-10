Drone plugin to detect files changed in a commit range.

# Usage

NOTE: This plugin writes to [DRONE_OUTPUT](https://developer.harness.io/docs/continuous-integration/troubleshoot-ci/ci-env-var/#drone_output) which is a feature of Harness CI.

To use this plugin in a Drone pipeline, you must manage the `DRONE_OUTPUT` file yourself. 

The following settings changes this plugin's behavior.

* param1 (optional) does something.
* param2 (optional) does something different.

Below is an example `.drone.yml` that uses this plugin.

```yaml
kind: pipeline
name: default

steps:
- name: run jimsheldon/drone-pathschanged plugin
  image: jimsheldon/drone-pathschanged
  pull: if-not-exists
  settings:
    param1: foo
    param2: bar
```

# Building

Build the plugin binary:

```text
scripts/build.sh
```

Build the plugin image:

```text
docker build -t jimsheldon/drone-pathschanged -f docker/Dockerfile .
```

# Testing

Execute the plugin from your current working directory:

```text
docker run --rm -e PLUGIN_PARAM1=foo -e PLUGIN_PARAM2=bar \
  -e DRONE_COMMIT_SHA=8f51ad7884c5eb69c11d260a31da7a745e6b78e2 \
  -e DRONE_COMMIT_BRANCH=master \
  -e DRONE_BUILD_NUMBER=43 \
  -e DRONE_BUILD_STATUS=success \
  -w /drone/src \
  -v $(pwd):/drone/src \
  jimsheldon/drone-pathschanged
```

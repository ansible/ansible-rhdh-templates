# backstage-templates

expected app-config configuration -
```
ansible:
  creatorService:
    baseUrl: 127.0.0.1
    port: '5000'
  devSpacesBaseUrl: >-
    https://devspaces.dummy.test-tests.testing.check.com/
```

## Add an execution environment to Controller

Register `all.yaml` in the Automation Portal catalog to make this template
available. For a disconnected deployment, mirror this repository to the
deployment’s GitHub or GitLab instance and register the mirrored `all.yaml`
location.

Open an execution environment image in Portal, pick a version, and select
**Use in Controller**. Start **Add execution environment to Controller** from
the filtered Templates list. The **Tag** field uses the Automation Content
plugin to list the selected image’s registry tags and display the resolved
digest. If you start the template directly, enter an image pull reference. Choose the Controller organization and
run the task with your signed-in AAP account. The completed task links to the
execution environment in Controller.

A command line tool for running GPT commands. This tool supports prompt-batching, prompt-chaining and ChatGPT Plugins.

## Features
Use this tool to
* Create **batch** processing of GPT requests. Run a set of data against a prompt and record the responses.
* Create **experiments** to see how different config parameters and prompts affect performance and output.
* Create **images** with DALL-E
* Do rapid prototyping of **ChatGPT Plugins** through a mock server

### Generate ChatGPT Plugin
The ChatGPT Plugin project allows you to do rapid prototyping of a ChatGPT Plugin. Specifically it
allows you to mock responses to ChatGPT. The project is based upon the quickstart project at: https://github.com/openai/plugins-quickstart

Your project file will look like

```yaml
---
projectName: plugin-quickstart
projectVersion: '1.0'
projectType: plugin
defaultConfig:
  properties:
    port: 5003
    nameForHuman: TODO Plugin (no auth)
    nameForModel: todo
    descriptionForHuman: Plugin for managing a TODO list, you can add, remove and view your TODOs.
  mockedRequests:
    - path: "/todos/global"
      method: get
      mockedResponse: todos-global.json
    - path: "/todos/user"
      method: get
      mockedResponse: todos-global.json

pluginServers:
  - serverId: todo-mike
    flavor: mike
    # mocked requests
    mockedRequests:
      - path: "/todos/mike"
        method: get
        mockedResponse: todos.json # returns the content of this file

  # Adds a different user for testing
  - serverId: todo-kaleb
    flavor: kaleb
    mockedRequests:
      - path: "/todos/kaleb"
        method: get
        mockedResponse: todos.json
        properties:
          showHttpHeaders: true # Show http headers in logs
```
Any configuration in the defaultConfig node will be applied to each pluginServer unless that plugin specifically
overrides the property.

A sample mocked response (_todos.json_) is given below. This will be returned on a call to **/todos/mike**

```json
{
  "todos": [
    "Clean out a septic tank",
    "Repair a broken sewer pipe",
    "Collect roadkill for disposal",
    "Assist in bee hive relocation",
    "Service a grease trap at a restaurant"
  ]
}
```
To start a mocked instance of the plugin server
```
air plugin
```
or to start a specific server add the _serverId_ option

```
air plugin --serverId todo-mike
```
For more information about creating and using a
[ChatGPT-Plugin](https://github.com/sisbell/stackwire-gpt/wiki/ChatGPT-Plugin)


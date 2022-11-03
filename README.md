# Let's Play with Spectral

_Spectral is an open source JSON/YAML linter, which allows you to create style guides for your structured data; things like OpenAPI/AsyncAPI/RAML descriptions, Kubernetes config, GitHub Actions, you name it, Spectral can help you lint it. Go beyond making sure they are "Technically Correct", make sure they are **useful**._

## Installation

You can install _Spectral_ using `npm` with the following commabd line using `npm`:

```text
npm install -g @stoplight/spectral-cli
```

Let's verifiy that the installation is correct with:

```text
spectral --version
```

## Getting Started

Let's use the following simple "Hello API" OpenAPI description:

```yaml
swagger: '2.0'
info:
  title: Hello API
  description: This is the documentation of the super awesome Hello API
  contact:
    name: Patrice Krakow
    email: patrice.krakow@gmail.com
  version: 0.1.0
basePath: /
paths:
  '/hello':
    get:
      summary: Get `hello`
      description: This API endpoint allows you to get the `hello`
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/Message'

definitions:
  Message:
    type: object
    properties:
      message:
        type: string
```

And let's implement the 1st rule that the `info.title` MUST end with the suffix " API":

```yaml
rules:
  title-api-suffix:
    description: The title of an API MUST end with the suffix " API".
    severity: error
    given: $.info.title
    message: The title "{{value}}" does not end with the suffix " API".
    then:
      function: pattern
      functionOptions:
        match: "\ API$"
```

## References

Stoplight. (n.d.). _Spectral, an Open Source JSON/YAML Linter_. Retrieved September 9, 2022, from <https://stoplight.io/open-source/spectral>

Stoplight. (n.d.). _JSON/YAML Linter with Custom Rulesets_. Retrieved September 9, 2022, from <https://github.com/stoplightio/spectral/blob/develop/README.md>

Stoplight. (n.d.). _Spectral Documentation_. Retreived November 3, 2022, from <https://docs.stoplight.io/docs/spectral>

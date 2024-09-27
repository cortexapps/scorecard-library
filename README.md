# Cortex.io Scorecard Library

A multi-purpose collection of scorecards that can be imported into your Cortex instance using the Cortex CLI

## General Info

Scorecards are kept in a YAML format with a .yaml suffix. This is the same format used when Scorecards are exported directly from the Cortex UI.

## Getting Started

In order to import these scorecards, you'll first need to have the [Cortex CLI](https://github.com/cortexapps/cli) running. Please follow [those instructions](https://github.com/cortexapps/cli/blob/main/README.rst) to prepare your environment!

## Importing Scorecards into Cortex

Once you have the CLI installed, you can run the following command to install any of the Scorecards in the [scorecard-definitions](https://github.com/cortexapps/scorecard-library/tree/master/scorecard-definitions) folder of this library:

```bash
cortex scorecards create -f [scorecard file]
```

For instance, to install the Incident Preparedness Scorecard, you could download the file directly (or of course clone the repo) and issue the following command:

```bash
cortex scorecards create -f incident-preparedness.cxs
```

The CLI will return an error if there's a problem, or a confirmation output in JSON. Note that each of the rules imported will be reflected in the "rules" array in the output, so be sure to validate that every rule was imported there:

```text
# cortex scorecards create -f vulnerability-management.cxs

{"scorecard":{"name":"Vulnerability Management","tag":"vulnerability-management-metrics","description":"Ensuring proactive identification and remediation of vulnerabilities","isDraft":false,"notifications":{"enabled":true},"exemptions":{"enabled":true,"autoApprove":false},"evaluation":{"window":4},"rules":[{"expression":"git.numOfVulnerabilities(severity=[\"CRITICAL\"]) == 0","weight":1,"description":"Ensure no critical vulnerabilities exist in the codebase or dependencies","title":"No Critical Vulnerabilities","failureMessage":null,"levelName":null,"effectiveFrom":null,"filter":{"types":null,"groups":null,"query":null},"identifier":"1a2b3c4d-5e6f-437a-b901-2d3e4f5a6b7c"}],"levels":null,"lastUpdated":"2024-09-27T18:51:21.85938","filter":{"types":{"include":["service"],"exclude":[]},"groups":null,"query":null}}}
```

Once the Scorecard is imported, it will be visible in the Scorecards interface in Cortex:

Scorecards -> Scorecards -> All

You can edit these Scorecards as normal once they have been imported, to further customize them for your use case.

## Contributing

If you'd like to share a scorecard, fork this repository and create a pull request. Please keep in mind the following guidelines:

- Clear any company-specific or otherwise identifiable information from all fields including Descriptions and comments
- The filename should match the 'tag' field in the YAML file, and file should be kept in a folder matching the 'name' field. Use the full 'yaml' suffix in the filename. You can provide additional documentation in this folder as needed
- It's ok to use comments in place of custom CQL rules, indicating that users should replace the field with their own corresponding CQL rule

We really appreciate your help growing this library!

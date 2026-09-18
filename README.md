# Relay HPC jobs

List your Slurm jobs on demand, including state, runtime, node count and pending reason.

The current implementation uses structured job rows with local text/state
filtering. Search controls stay visible while the job list scrolls. At most 500
rows are loaded, with the observed queue count and an explicit partial-results
notice. Filters apply only to loaded rows. Missing Slurm, unavailable schedulers,
malformed rows and incompatible helpers produce errors rather than an empty list.

Component verification covers parser/limit/failure cases, package lifecycle,
an actual scheduler query and manual native-UI search/filter/empty/large-queue
checks. Installed-app and wheel/trackpad acceptance are still outstanding;
this is not a release-ready claim.

## Status and compatibility

Experimental native-tool package. Requires the Relay build that implements
the `tool` contribution and the matching `relayd plugin` helper. Older Relay
builds reject this package safely. This is a data-only package: the implementation
lives in [Relay](https://github.com/genomewalker/relay-terminal), not executable
code downloaded from this repository. No install hooks or background polling.

The native implementation is under development and has not yet passed installed-app
acceptance. Do not mistake a manifest for a production-ready extension.

## Install and use

When a tagged release is available, open Relay Settings → Plugins, enter
`genomewalker/relay-plugin-hpc-jobs` and its exact tag, review the digest and
permissions, install disabled, then Enable. Select a terminal pane and open
the puzzle-piece button in the workspace toolbar. Select this tool, verify the
host/directory, and choose **Allow once & refresh**. Each refresh is explicit.

Updates require another reviewed version and start disabled. Disable, Roll back
and Uninstall are available in Settings. Safe mode suppresses all plugin tools.

## Limits

Slurm must be installed on the selected host. Job logs, resource history, submission and cancellation are not implemented.

The captured pane selects the connection; switching tabs does not retarget
an in-flight request. Jobs belong to the connected user across all projects,
not only the selected directory. Remote hosts need a matching helper installed through Relay's
existing approved setup flow. Agent processes are never restarted by this plugin.

## Package verification

```sh
python3 -m json.tool relay-plugin.json
```

Runtime, path-containment, payload-integrity and permission tests live alongside
the implementation in Relay. Publish `relay-plugin.json` as a release asset only
after those tests and the corresponding installed-app acceptance checks pass.

## License

No license has been selected yet. Public visibility does not grant a reuse license.

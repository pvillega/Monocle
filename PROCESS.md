## Process

### Introduction

This document is intended to help consolidate the practices we are
using to develop and maintain Monocle. Its primary audience is Monocle
maintainers who may need to close issues, merge PRs, do releases, or
understand how these things work.

### Merging pull requests

Pull requests currently require one sign-off from Monocle maintainer 
(which must be different from the pull request author). Community member 
sign-offs are appreciated as votes of confidence but don't usually 
count.

When fixing typos, improving documentation or other minor changes 
no sign-off is required if no Monocle maintainer comment on the pull 
request after one day.

For serious emergencies or work on the build which can't easily be
reviewed or tested, pushing directly to master may be OK (but is
definitely not encouraged). In these cases it's best to comment in
Gitter or elsewhere about what happened and what was done.

### Versioning

If a release is simply a bug fix, increment the patch version number
(e.g. 1.2.3 becomes 1.2.4). These releases may happen quite quickly in
response to reported bugs or problems, and should usually be source
and binary compatible.

Significant additions should increment the minor version number 
(e.g. 1.2.3 becomes 1.3.0) and breaking or incompatible changes should 
increment the major number (e.g. 1.2.3 becomes 2.0.0). These major version 
bumps should only occur after substantial review, warning, and with proper 
deprecation cycles.

### Releasing

Before the release, the tests and other validation must be passing.

Currently, the best way to release Monocle is:

 1. Run `+ clean` to ensure a clean start.
 2. Run `+ package` to ensure everything builds.
 3. Run `release`, which will validate tests/code, etc.

(Eventually `release` should do all of these things but for now the
individual steps are necessary.)

You will need to enter a GPG password to sign the artifacts correctly,
and you will also need to have Sonatype credentials to publish the
artifacts. The release process should take care of everything,
including releasing the artifacts on Sonatype.

If the Sonatype publishing fails, but the artifacts were uploaded, you
can finish the release manually using the Sonatype web site. In that
case you will also need to do `git push --tags origin master` to push
the new version's tags.

### Post-release

After the release occurs, you will need to update the
documentation. Here is a list of the places that will definitely need
to be updated:

 * `docs/src/site/index.md`: update version numbers
 * `README.md`: update version numbers
 * `docs/src/site/release_note.md`: update release note

(Other changes may be necessary, especially for large releases.)

You can get a list of changes between release tags `v0.1.2` and
`v0.2.0` via `git log v0.1.2..v0.2.0`. Scanning this list of commit
messages is a good way to get a summary of what happened, although it
does not account for conversations that occurred on Github.

### Conclusion

Ideally this document will evolve and grow as the project
matures. Pull requests to add sections explaining how maintenance
occurs (or should occur) are very welcome.
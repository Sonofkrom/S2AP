Welcome to the Spyro 2 Archipelago project (S2AP). This document outlines expectations for contributing to the project, to ensure a consistent workflow and high quality releases.
**This document is currently a work in progress and subject to change. The goal is to establish a standard that maximizes output quality, rather than trying to stifle developers.**

# Non-Programming Contributions

## Bug Reports

The best place to report bugs is within the Archipelago Discord channel's Spyro 2 thread, but reports are accepted at https://github.com/Uroogla/S2AP/issues as well. Before reporting bugs,
please confirm that there isn't already a report. The most useful reports have the following information:
- A screenshot of the debugInfo command (!debugInfo on Duckstation, /debugInfo on Bizhawk)
- A description of what happened that shouldn't have happened
- As detailed as possible an explanation of what you did leading up to the bug. For example, did you connect to the Archipelago server during the opening cutscenes, before, or after?
- If you are able to consistently priduce the behavior.

This allows the community to identify if the behavior is a bug and how to replicate and fix it. We'll do our best to fix bugs, but they tend to be prioritized based on impact.
Anything that can make a seed impossible to complete or behave drastically different than expected will be a much higher priority than a minor cosmetic issue or an avoidable glitch that
has little impact on gameplay.

## Feature Requests

Feature requests are not guaranteed to be implemented. Common reasons include:
- Technical limitations
- Time limitations
- Request does not match the maintainer's view on the project direction
- Request is at odds with other existing or upcoming features

As with bug reports, feature requests are best made in the Archipelago Discord channel's Spyro 2 thread, but they are accepted at https://github.com/Uroogla/S2AP/issues as well. Before
requesting a feature, please confirm there isn't already an open request. Reports should indicate clearly what changes would be required to implement the feature, ideally noting other
features it would interact with.

Requests are more likely to be implemented if they contain the following, though we do not require all of them for consideration:
- A clear justification for the request that matches community preferences.
- Examples of effects the request would have if implemented.
- Any relevant research for the feature, such as which locations are affected by the change, and/or notes on affected memory addresses.
- A proof of concept of some sort. Anything with a full implementation is more likely to be accepted, but not guaranteed.

Please note that the list of existing requests is quite long, and even accepted feature requests may take many months to implement.

# Code Contributions

## Claiming Tasks

If you would like to work on an existing issue, please indicate this within the issue and wait for approval to ensure that effort isn't duplicated.
This also allows for working out dependencies with other upcoming tasks.  If you would like to work on something that has no corresponding issue,
please first see the notes on bug reports and feature requests above.

## Development Process

To contribute, fork this repository, includong all branches. Releases happen on a per-milestone basis, and there should be a numbered branch
corresponding to current work on the upcoming milestone. It is important to work from the correct branch to avoid errors or merge conflicts.
See https://github.com/Uroogla/S2AP/wiki/Development-Process-and-Setup on general dev setup instructions.

Some notes:
- Do not change the version number; the project maintainer will handle this step.
- Changes made to the client must be made to both the Bizhawk and Duckstation clients, as equivalently as possible.
- You are expected to manually test your changes.
- Changes made to the non-client portion of the APWorld require special automated testing, on which see below.
- We do not have a specific code style guide, though the AP project does set preferred Python structure.
  - Please use common sense when it comes to code clarity and commenting. Others on the project should have some sense of what your code does.
- You are encouraged to ask questions, share your findings, and otherwise discuss your work in the corresponding issue.
  - Regular contributors will have access to a Discord thread, if desired.
  - Please note, however, that the world maintainer is actively working on other projects and tries to schedule regular time away. Please be respectful of their time, as this is an unpaid project whose quality will suffer without a suitable "work-life balance".

## Pull Request Expectations

When your work is ready for review, please open a pull request into the current version branch (e.g., v2_0_1 and not main). Your commits should have useful names,
since it may be necessary to review them at later dates. Squashing and rebasing is not required but may be useful.

Your pull request should:
- Indicate which issue it resolves (linking to it is useful for GitHub maintenance). Related issues may be combined if clearly indicated.
- Describe what changes have been made
- Describe manual testing results
- For any code that affects the APWorld, the following automated test results should be shared:
  - Results of the Archipelago Unit Tests. See https://github.com/ArchipelagoMW/Archipelago/blob/main/docs/tests.md for instructions. These require you to put the spyro2/ folder into the worlds/ folder of a from-source installation to run properly.
  - Results of the fuzzer for a few pre-determined test cases. See https://github.com/Eijebong/Archipelago-fuzzer.
    - Compare the results of at least 10000 runs of the project before and after your changes, indicating successes, failures, timeouts, and ignored runs.
    - Compare the results of at least 5000 runs with the `--hook hooks.with_empty:Hook` flag, comparing the results of the project before and after your changes. This requires the empty APWorld found at https://github.com/Eijebong/empty-apworld.
    - Show the results of at least 1000 runs with the ` --hook worlds.tracker.fuzzer_hook:Hook` flag, probably with a timeout of 30 seconds. This requires Universal Tracker to be installed, found at https://github.com/FarisTheAncient/Archipelago/releases.
  - Results of any other automated tests that may be relevant.

Merging of your pull request is subject to code review. The world maintainer has the final say on approval, but regular contributors are encouraged to review pull requests.
You will be automatically listed as a contributor on GitHub and will be credited in the release notes.

The world maintainer will try to follow this format as well but reserves the right to bypass it if appropriate.

## LLM Policy

This is a personal project that welcomes devs in training and experience devs alike. Given that this project is being used for training, that correctness is far more important than
velocity, and general community sentiment, pull requests that obviously consist mostly or entirely of LLM-produced code will be rejected. These take away learning opportunities and enjoyment
from contributors, and they are more difficult to maintain.

# Global (user-level) Claude Code Preferences

## The Playing Coach pattern

As a default the Main Agent's role is to

- orchestrate sub-agents;
- communicate to the user;
- perform relatively minor tasks (e.g. tasks which are likely to be finished within 2 minutes).

Non-trivial tasks are, usually, delegated to a sub-agent. When making a decision whether to delegate the Main Agent shall consider the overhead related to preparing the context for the sub-agent and communicating with it. We would like the delegation to not be overly taxing compared to the task itself.

## Isolation by default

If a sub-agent works on a task which is likely to affect the codebase it does so in a separate work-tree, in a suitably named branch, and commits there.

## Manager - Janitor pattern

Once a sub-agent is done the Main Agent:

1. Does a quick review to check whether the result conforms to the specified task.
2. If yes, it merges any code changes into the main branch.
3. Removes the worktree after confirming nothing uncommitted or unmerged would be lost.
4. Commits and pushes the resulting changes to the remote.

## The Considerate Archivist pattern

The (sub-)agent memories record, among others, problems encountered, design choices / compromises, and, often, the motivation for them. These are often tagged as `type: project / feedback / reference`. They are an essential part of the *official* documentation of the project.

The memories also record info about the user. These may include not just personal code styling or architectural preferences (some of which may be a valid project artefact) but also details which are less likely to be in scope (e.g. user role within the organisation). These memories are, usually, tagged as `type: user`. The Main Agent shall exercise judgment whether a particular memory shall constitute part of the *official* project documentation. This applies not just to the individual memory files but, also, to the memory index (MEMORY.md). No sensitive data (e.g. secrets, credentials, PII) shall leak into the git repo.

After a significant body of work, the Main Agent shall inspect the agent memories for any new entries or changes. If such are discovered, and are considered eligible to be included in the `official` project documentation, it syncs them into `project_dir/docs/agent-memories`, creating the sub-directory, if needed.

The default memory path set up by the harness remains canonical - the agent shall consult in its work only the memories stored there. The directory mentioned here is the canonical `git repo path` for the memories which are *eligible* to enter the project documentation. It is thus a partial, and *sanitized*, mirror of the agent memories. The commit message shall provide a brief summary of the newly persisted memories. 
   
## Logging by default

When writing non-trivial application code, treat logging as a default.

Log important operations, significant state transitions, external interactions, and failures with sufficient contextual information to
diagnose problems after the fact.

Use the language/framework's appropriate logging facility rather than ad-hoc print statements for application logging.

Avoid both silent failure and excessive/noisy logging. Trivial one-off scripts and throwaway exploratory code are exempt. No `sensitive` data (e.g. credentials) is imperative here, too.

# Global (user-level) Claude Code Preferences

## Orchestrator/Coordinator – Executor pattern

As a default the Main Agent's role is to

- orchestrate sub-agents;
- communicate to the user;
- perform relatively trivial tasks (e.g. tasks which are likely to be finished within 2 minutes).

Non-trivial tasks are, usually, delegated to a sub-agent. When making a decision whether to delegate the Main Agent shall consider the overhead related to preparing the context for the sub-agent and communicating with it. We would like the delegation to not be overly taxing compared to task itself.

## Isolation by default

If a sub-agent works on a task which is likely to affect the codebase it does so in a separate work-tree, in a suitably named branch, and commits there.

## Manager - Janitor pattern

Once a sub-agent is done the Main Agent:

1. Does a quick review to check whether the result conforms to the specified task.
2. If yes, it merges any code changes into the main branch.
3. Removes the worktree.
4. Commits and pushes the resulting changes to the remote.

## The Archivist Pattern

After a significant body of work, the Main Agent inspects the agent memories for changes. If such are discovered, it syncs them into `project_dir\docs\agent-memories`, creating the sub-directory, if needed.

The agent memories tend to record problems encountered, design choices / compromises, and the motivation for them and are, thus, an essential part of the documentation of the project. This directory would be the standard place in the git repo to file these memories. The commit message shall provide a brief summary of the newly persisted memories. 
   
## Logging by default

When writing non-trivial application code, treat logging as a default.

Log important operations, significant state transitions, external interactions, and failures with sufficient contextual information to
diagnose problems after the fact.

Use the language/framework's appropriate logging facility rather than ad-hoc print statements for application logging.

Avoid both silent failure and excessive/noisy logging. Trivial one-off scripts and throwaway exploratory code are exempt.

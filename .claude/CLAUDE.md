# Global (user-level) Claude Code Preferences

## Subagent isolation

When working in a git repository, any subagent or sub-task that will
modify files must operate in its own git worktree on its own
descriptively named branch.

The subagent commits its work in that worktree.

When the work is complete, the orchestrating agent:
1. merges the branch into the appropriate main branch;
2. pushes the result to the remote;
3. removes the worktree after confirming that no unmerged or
   uncommitted work would be lost.

This applies whether one or multiple subagents are running.

## Observability by default

When writing non-trivial application code, treat logging and
observability as a default.

Log important operations, significant state transitions, external
interactions, and failures with sufficient contextual information to
diagnose problems after the fact.

Use the language/framework's appropriate logging facility rather than
ad-hoc print statements for application logging.

Avoid both silent failure and excessive/noisy logging. Trivial
one-off scripts and throwaway exploratory code are exempt where
logging would add disproportionate overhead.

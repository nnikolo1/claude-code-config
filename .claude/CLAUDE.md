# Global (user-level) Claude Code Preferences

## Orchestrator/Coordinator – Executor pattern

By default the main agent is used to orchestrate the sub-agents and communicate to the user. Delegate each file modification task to a sub-agent. If research is non-trivial, delegate it to a sub-agent, too. The main agent shall spawn the sub-agents and integrate / cleanup after them.

When a sub-agent is expected to modify code it must operate in its own git worktree on its own descriptively named branch. The subagent commits its work in that worktree.

When the work is complete, the main agent:
1. merges the branch into the appropriate main branch;
2. removes the worktree after confirming that no unmerged or uncommitted work would be lost;
3. synchronizes the project's agent memories from Claude Code's user-level memory directory into `project/docs/agent-memories/`, creating the directory if necessary;
4. commits and pushes the resulting changes to the remote.
   
## Observability by default

When writing non-trivial application code, treat logging and observability as a default.

Log important operations, significant state transitions, external interactions, and failures with sufficient contextual information to
diagnose problems after the fact.

Use the language/framework's appropriate logging facility rather than ad-hoc print statements for application logging.

Avoid both silent failure and excessive/noisy logging. Trivial one-off scripts and throwaway exploratory code are exempt where
logging would add disproportionate overhead.

# Investigation handoff

You are continuing Lattence, an AI security and post-quantum security assurance
platform. Its central behavior is correlating AI findings and cryptographic
findings over real edges in one security graph.

## Establish the actual checkout

1. Run pwd, git remote -v, git status --short --branch, git rev-parse HEAD,
   and git log -5 --oneline. Confirm origin is Vishnu2707/lattence.
2. Read AGENTS.md, agent.md, BUILD/STATE.md, BUILD/TASKS.md, BUILD/PROTOCOL.md,
   the owning role, and relevant module notes. Inspect contracts and design
   only as needed to verify acceptance. Do not overwrite frozen contracts.
3. Fetch origin. Compare origin/main and origin/dev. As of this handoff,
   main is 2417e232 and latest work is dev at cc0aea7. Do not assume main
   contains the reported follow-up work. Work on dev. Preserve existing changes.
4. Select a new ledger task for the investigation. Keep scope to this bug.

## Reproduce before editing

Create a fresh disposable checkout and a Python 3.12 environment. Use the
repository's supported installation procedure, including all workspace members
for source verification: uv sync --all-packages --dev. Also build a wheel and
install it into a separate clean environment for final package acceptance.
Confirm imports and executables resolve to the intended checkout or wheel,
never a stale public package. Record full SHA, Python version, dependency
versions, exact install commands, and any network or installation blockers.

Use the real examples/vulnerable-agent fixture. Derive CLI syntax from help
and repository notes. Copy only tracked fixture files to a fresh temporary
folder outside the repository. Record its file list and hashes. Keep baseline
reports outside that folder. Capture raw scan output and JSON, node counts,
edge counts, attack path counts, chain correlations, distinct structural paths,
and bytes of each output artifact. Record exit codes; a findings gate exit
is not an execution failure.

The user reports 20,684 paths instead of approximately 92. Both numbers are
claims to investigate, not acceptance constants. Run a second scan without
changing fixture source. Separately test reports written inside the fixture
and repeated scans. Compare source and packaged behavior. If the issue cannot
be reproduced, report the precise revision, environment, fixture, and commands
that differ; do not silently declare the issue fixed.

## Trace the root cause

Instrument discovery, graph assembly, and path traversal. Identify the first
function where counts diverge. Inspect source selection, generated artifact
exclusion, duplicate identities, repeated relationships, direction handling,
and path enumeration. Show concrete unexpected nodes or edges, their source
files, and the call path that creates them. Do not cap output or hide paths
as a substitute for correcting graph construction or traversal semantics.

Write a focused regression test that fails before the fix and passes after.
Cover the triggering fixture condition, repeat-scan stability, and a valid
security path that must remain discoverable. Explain why the corrected counts
follow from actual entities and relationships rather than the README number.
Make the smallest fix. Run scoped checks and the owning role's verification.

## Independently verify the disputed work

After the fix, reproduce from a fresh checkout and freshly installed wheel.
Show before and after commands and output. Verify:

- Stable node, edge, and path counts; report sizes and output exclusions.
- The self-contained dashboard: findings table, PQC score, chain view,
  realistic byte size, and useful visible content. Separate truncation from
  graph correctness. Confirm no external asset dependency.
- Cross-layer correlations versus distinct structural paths, real stored
  graph edges, traversal orientation, source evidence, and consistency across
  terminal, JSON, HTML, and other supported renderers. Preserve the real
  LT-AI-002 to LT-PQC-203 example where valid. Historical 32/9 counts require
  fresh verification, not copied assertions.
- The CI template's real commands, valid SARIF results, artifacts, and severity
  gate exit code. Distinguish local shell verification from a real hosted
  pipeline run. Do not claim a hosted run without its actual evidence.

Track any independently discovered issue as a separate task. Do not bundle
new features or the pre-commit prose gap into the graph fix. After correctness
is established, prioritize the dashboard, chain reporting, and pre-commit prose
checking, then language coverage and integrations.

## Evidence and completion

Store large logs under BUILD/logs/, and record reproducible commands and a
concise result table in tracked module notes. Label every item verified,
unverified, blocked, or failed. Include root-cause function and lines, changed
files, regression test, before/after counts, artifact sizes, and remaining gaps.
Update agent.md, BUILD/STATE.md, BUILD/TASKS.md, module notes, and decisions
in the same task commit. Follow repository authorship and prose rules. Use
one task per commit on dev, push to origin/dev, and verify synchronization.
Do not push directly to main, release, publish, deploy, or merge a milestone
as part of this investigation. If push fails, report the blocker accurately.

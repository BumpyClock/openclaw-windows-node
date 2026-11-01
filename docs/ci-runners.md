# CI runner migration

Portable GitHub Actions Linux jobs use Boat, including path classification, CI Gate, CodeQL Actions/advanced-setup gate, Copilot setup, triage, stale/lock automation, ClawSweeper dispatch and daily alpha orchestration. Existing upstream/version/release conditions, classification values, full-history requirements, permissions, outputs and release dependencies remain unchanged. No workflow is dispatched by this source change.

Boat's tested Ubuntu 24.04 x64 image lacks `pwsh`. The two portable PowerShell jobs use `.github/actions/setup-linux-powershell` after checkout and before their first PowerShell step. It installs PowerShell 7.6.9 from the official release into runner-temporary storage, checks its SHA-256 digest and version, then updates the job PATH. `scripts/test-ci-workflow-contract.ps1` checks that ordering. Native Windows x64/ARM64, signing, packaging, UI and E2E jobs are unchanged.

BumpyClock owner-only public Boat execution is approved. Outside contributors and bots remain blocked by account policy, including bot-authored fork automation. Do not remove trust/release guards to bypass policy. Copilot's self-hosted execution additionally requires compatible repository firewall/network policy; no firewall or account settings are changed here. See [GitHub's Copilot environment requirements](https://docs.github.com/en/copilot/how-tos/agents/copilot-coding-agent/customizing-the-development-environment-for-copilot-coding-agent).

Portable workflow/detector tests do not qualify the Windows application. Full build, shared/tray tests, MSIX, UI and E2E acceptance still require the supported Windows host. No new features, hooks, billing/auth repair or native runner purchase is included.

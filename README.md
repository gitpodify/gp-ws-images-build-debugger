# Gitpodified Workspace Images Build Debugger

## Connecting to the bulldozer

To make connections to the GitHub Actions worker where the build debugging SSH server is running, you need to install Tailscale locally on your machine and be member of Recap Time GitHub org. For the authentication process to run smoothly, you need to add your ephemeral Tailscale auth key as either Codespaces encrypted secret on your GitHub account or as an use rvariable in Gitpod with variable name `TAILSCALE_AUTHKEY_RECAPTIME`.

1. Open this repository in GitHub Codespaces or Gitpod.
2. Wait for the build to complete and the web editor to load up.
3. Open the terminal and check if you're authenticated against our tailnet with `tailscale status`. If not, try again with `tailscale up --authkey="your-auth-key" --hostname=$HOSTNAME`.
4. Load up your private SSH key into the SSH agent via `ssh-add` command and then connect to the debugger with `ssh runner@$(tailscale ip -4 gp-ws-images-bulldozer-gha)`. Happy debugging!

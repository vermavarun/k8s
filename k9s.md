# K9s - Kubernetes CLI To Manage Your Clusters

K9s is a terminal-based UI to interact with your Kubernetes clusters. It provides a fast and efficient way to navigate, observe, and manage applications.

---

## 📋 Installation

```bash
# macOS
brew install derailed/k9s/k9s

# Linux
curl -sS https://webinstall.sh/k9s | bash

# Windows
choco install k9s
```

---

## 🎯 Basic Navigation & Commands

| Key/Command | Description |
|------------|-------------|
| `:` | Command mode - type resource name (e.g., `:pod`, `:svc`, `:deploy`) |
| `?` | Show help/keyboard shortcuts |
| `Ctrl+a` | Show all available resources |
| `Ctrl+c` | Exit/Quit k9s |
| `/` | Filter mode - filter resources by name |
| `Esc` | Exit current mode/view |
| `Enter` | View resource details/logs |
| `Ctrl+r` | Refresh current view |

---

## 🔍 Resource Navigation Shortcuts

| Shortcut | Resource | Alternative |
|----------|----------|-------------|
| `:pod` | Pods | `:po` |
| `:deploy` | Deployments | `:deployment` |
| `:svc` | Services | `:service` |
| `:ns` | Namespaces | `:namespace` |
| `:node` | Nodes | `:no` |
| `:cm` | ConfigMaps | `:configmap` |
| `:secret` | Secrets | - |
| `:ing` | Ingress | `:ingress` |
| `:pv` | Persistent Volumes | - |
| `:pvc` | Persistent Volume Claims | - |
| `:sa` | Service Accounts | - |
| `:job` | Jobs | - |
| `:cj` | CronJobs | `:cronjob` |
| `:ds` | DaemonSets | `:daemonset` |
| `:sts` | StatefulSets | `:statefulset` |
| `:rs` | ReplicaSets | `:replicaset` |
| `:netpol` | Network Policies | - |
| `:hpa` | Horizontal Pod Autoscaler | - |
| `:pdb` | Pod Disruption Budget | - |
| `:ctx` | Contexts | - |
| `:cr` | Custom Resources | - |

---

## ⚡ Action Keys (When Resource is Selected)

| Key | Action | Description |
|-----|--------|-------------|
| `d` | Describe | Show detailed resource information |
| `l` | Logs | View container logs |
| `e` | Edit | Edit resource YAML |
| `y` | YAML | View resource YAML |
| `s` | Shell | Execute shell into container |
| `Ctrl+d` | Delete | Delete selected resource |
| `p` | Previous logs | View logs from previous container |
| `f` | Port-forward | Forward local port to pod |
| `t` | Attach | Attach to running container |
| `w` | Wrap | Toggle log line wrapping |
| `c` | Copy | Copy resource name to clipboard |
| `Ctrl+k` | Kill | Force delete pod |
| `z` | Toggle wide | Show/hide additional columns |
| `0` | Show all logs | View all logs (no filtering) |

---

## 📊 View & Display Options

| Key | Function | Description |
|-----|----------|-------------|
| `Spacebar` | Mark/Unmark | Select multiple resources |
| `Tab` | Switch focus | Move between panes |
| `h` | Toggle header | Show/hide column headers |
| `z` | Toggle wide columns | Show additional information |
| `Ctrl+s` | Save | Save current resource |
| `u` | Toggle used resources | Show resources in use |
| `n` | Toggle namespaces | Filter by namespace |
| `0-9` | Select container | Choose container in multi-container pod |

---

## 🔎 Filtering & Searching

| Key/Command | Function | Description |
|------------|----------|-------------|
| `/filter` | Filter | Filter resources by name/label |
| `Ctrl+u` | Clear filter | Remove current filter |
| `/!` | Inverse filter | Show everything except match |
| `/-l label=value` | Label filter | Filter by label selector |
| `Ctrl+/` | Fuzzy search | Enable fuzzy searching |

### Filter Examples:
```
/nginx              # Filter for resources containing "nginx"
/!system            # Exclude resources with "system"
/-l app=frontend    # Filter by label app=frontend
```

---

## 📝 Log Management

| Key | Function | Description |
|-----|----------|-------------|
| `l` | View logs | Show container logs |
| `p` | Previous logs | Logs from previous container instance |
| `c` | Clear logs | Clear current log buffer |
| `s` | Toggle auto-scroll | Auto-scroll to latest logs |
| `w` | Toggle wrap | Wrap long log lines |
| `f` | Toggle fullscreen | Expand log view |
| `t` | Toggle timestamps | Show/hide timestamps |
| `Ctrl+s` | Save logs | Save logs to file |
| `0-9` | Container select | Select container in multi-container pod |
| `/` | Filter logs | Search within logs |

---

## 🎛️ Context & Namespace Management

| Command | Function | Description |
|---------|----------|-------------|
| `:ctx` | List contexts | View and switch Kubernetes contexts |
| `:ns` | List namespaces | View and switch namespaces |
| `Enter` (on context/ns) | Switch | Switch to selected context/namespace |
| `Ctrl+n` | Next namespace | Cycle to next namespace |
| `Ctrl+p` | Previous namespace | Cycle to previous namespace |

---

## 🔧 Advanced Commands

| Command | Description |
|---------|-------------|
| `:xray [resource]` | Show resource relationships and dependencies |
| `:popeye` | Run cluster sanity checks |
| `:pulses` | View cluster pulse/metrics |
| `:screendump` | Take screenshot of current view |
| `:bench` | Run benchmarks on resources |
| `:alias` | Manage k9s aliases |

---

## 🎨 Customization & Configuration

### Config File Location:
- **Linux/macOS**: `~/.config/k9s/config.yml`
- **Windows**: `%APPDATA%\k9s\config.yml`

### Useful Config Options:

```yaml
k9s:
  refreshRate: 2          # Refresh interval in seconds
  maxConnRetry: 5         # Max connection retries
  readOnly: false         # Enable read-only mode
  noExitOnCtrlC: false    # Don't exit on Ctrl+C
  ui:
    enableMouse: false    # Enable mouse support
    headless: false       # Run without UI
    logoless: false       # Hide k9s logo
    crumbsless: false     # Hide breadcrumbs
  skipLatestRevCheck: false
  logger:
    tail: 100            # Number of log lines to tail
    buffer: 5000         # Log buffer size
    sinceSeconds: 60     # Logs since (seconds)
    textWrap: false      # Wrap log lines
    showTime: false      # Show timestamps
```

---

## 🔑 Custom Hotkeys

You can create custom hotkeys in `~/.config/k9s/hotkey.yml`:

```yaml
hotKey:
  # Shift+0 to view all resources
  shift-0:
    shortCut: Shift-0
    description: View all
    command: all
  # Shift+p to view pods
  shift-p:
    shortCut: Shift-P
    description: View pods
    command: pods
```

---

## 🎯 Quick Reference Workflow

### Typical k9s Workflow:

1. **Start k9s**: `k9s`
2. **Navigate to resource**: `:pod`
3. **Filter**: `/my-app`
4. **Select pod**: Arrow keys + Enter
5. **View logs**: `l`
6. **Shell into pod**: `s`
7. **Edit resource**: `e`
8. **Delete resource**: `Ctrl+d`
9. **Exit**: `Ctrl+c`

---

## 💡 Pro Tips

| Tip | Description |
|-----|-------------|
| **Bookmark commands** | Use aliases for frequent commands |
| **Read-only mode** | Start with `k9s --readonly` for safety |
| **Specific context** | Launch with context: `k9s --context prod` |
| **Specific namespace** | Start in namespace: `k9s -n kube-system` |
| **Log following** | Logs auto-scroll by default, toggle with `s` |
| **Batch operations** | Use spacebar to select multiple, then perform action |
| **Screen recordings** | Use `:screendump` for documentation |
| **Cluster health** | Run `:popeye` regularly for cluster sanity |
| **Resource relationships** | Use `:xray deploy` to see deployment dependencies |

---

## 🚀 Starting k9s

```bash
# Default - current context
k9s

# Specific context
k9s --context production

# Specific namespace
k9s -n kube-system

# Read-only mode
k9s --readonly

# All namespaces
k9s -A

# Specific cluster
k9s --kubeconfig ~/.kube/custom-config

# With command
k9s -c pod

# Headless mode (for scripting)
k9s --headless
```

---

## 📚 Additional Resources

- **Official Docs**: https://k9scli.io
- **GitHub**: https://github.com/derailed/k9s
- **Slack**: Kubernetes #k9s channel

---

**Last Updated**: January 2026

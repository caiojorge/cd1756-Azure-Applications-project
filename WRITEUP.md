# Write-up

### Analyze, choose, and justify the appropriate resource option for deploying the app.

**Virtual Machine (VM)**
- **Costs:** Higher — you pay for the VM even when idle, and you are responsible for OS maintenance and updates.
- **Scalability:** Manual — requires configuring load balancers and scale sets yourself.
- **Availability:** You are responsible for setting up redundancy and failover.
- **Workflow:** Manual deployment (SSH, scripts); more control, but higher operational overhead.

**App Service**
- **Costs:** Lower — you pay for the service plan; free/basic tiers are available for lightweight apps.
- **Scalability:** Automatic — scale out based on CPU/memory without managing infrastructure.
- **Availability:** High availability and health checks are managed by Azure.
- **Workflow:** Deploy via GitHub Actions directly to App Service, with no OS or server management required.

**Choice: App Service**

App Service is the right choice for this Flask CMS. The app is lightweight and stateless (sessions on filesystem, data in Azure SQL and Blob Storage) with no special OS or hardware requirements. App Service removes operational overhead and integrates natively with the GitHub Actions pipeline already configured in the project.

---

### Assess app changes that would change your decision.

I would switch to a VM if the app required:

- **Heavy computation** (e.g. video transcoding, ML inference) — GPU-enabled VMs are better suited for this.
- **Custom system-level software** — native drivers, libraries, or OS configurations not supported by App Service.
- **Full network control** — granular firewall rules, complex site-to-site VPN, or non-HTTP ports.
- **Persistent local state** — if the app relied on disk files between requests (App Service warns that data outside `/home` is not persisted).

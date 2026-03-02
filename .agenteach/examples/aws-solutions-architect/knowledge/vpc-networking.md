# VPC Networking

> Status: 📖 in progress
> Exam domain: Design Resilient Architectures (30%)

---

## What is a VPC

A Virtual Private Cloud is your own isolated network inside AWS. Think of it as renting a floor in a data center — you control the layout, doors, and security cameras, but Amazon owns the building.

**Key parameters:**
- CIDR block: defines the IP range (e.g., `10.0.0.0/16` = 65,536 IP addresses)
- Region: a VPC lives in one AWS region
- Default VPC: AWS creates one per region automatically. For production, create custom VPCs.

---

## Subnets

Subnets divide a VPC into smaller networks. Two types:

| Type | Internet access | Use case |
|------|----------------|----------|
| **Public subnet** | Yes (via Internet Gateway) | Web servers, load balancers |
| **Private subnet** | No direct access | Databases, app servers |

**Worked example — 3-tier architecture:**
```
VPC: 10.0.0.0/16

Public subnet:  10.0.1.0/24  (256 IPs) → web tier (ALB, web servers)
Private subnet: 10.0.2.0/24  (256 IPs) → app tier (application servers)
Private subnet: 10.0.3.0/24  (256 IPs) → data tier (RDS, ElastiCache)
```

The web tier faces the internet. The app tier only talks to the web tier. The data tier only talks to the app tier. Each layer is isolated.

---

## Route Tables

Every subnet has a route table that controls where traffic goes.

**Public subnet route table:**
| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | local (stays in VPC) |
| 0.0.0.0/0 | igw-xxxx (Internet Gateway) |

**Private subnet route table:**
| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | local |
| 0.0.0.0/0 | nat-xxxx (NAT Gateway, for outbound only) |

The key difference: public subnets route `0.0.0.0/0` to an Internet Gateway, private subnets route to a NAT Gateway (outbound only, no inbound from internet).

---

## Security Groups vs NACLs

Two layers of firewall:

| Feature | Security Group | NACL |
|---------|---------------|------|
| Level | Instance (ENI) | Subnet |
| State | **Stateful** — return traffic auto-allowed | **Stateless** — must explicitly allow both directions |
| Default | Deny all inbound, allow all outbound | Allow all both directions |
| Rules | Allow only (no deny rules) | Allow AND deny rules |
| Evaluation | All rules evaluated together | Rules evaluated in order (lowest number first) |

**The stateful vs stateless distinction is the most common exam question:**
- Security Group: if you allow inbound port 443, the response is automatically allowed out.
- NACL: if you allow inbound port 443, you MUST also add an outbound rule for ephemeral ports (1024-65535), or the response will be blocked.

---

## Terminology

| Term | Meaning |
|------|---------|
| CIDR | Classless Inter-Domain Routing — notation for IP ranges (e.g., /16 = 65,536 IPs) |
| IGW | Internet Gateway — allows public subnet traffic to reach the internet |
| NAT Gateway | Network Address Translation — lets private subnets make outbound internet requests |
| ENI | Elastic Network Interface — virtual network card attached to an instance |
| Ephemeral ports | Temporary ports (1024-65535) used for response traffic |

---

## Common Exam Scenarios

**Scenario 1:** "A company needs web servers accessible from the internet and a database that should never be directly reachable from outside."
→ Public subnet for web servers (with Security Group allowing port 80/443), private subnet for database (Security Group allowing only the web server's SG as source).

**Scenario 2:** "Two VPCs in different regions need to communicate privately."
→ VPC Peering (same region or cross-region). Traffic stays on AWS backbone, never touches the internet.

---

## Dziennik nauki

Chronological record of the learning process. The agent uses these entries to plan future questions and explanations.

### 2026-02-24

- **Question:** What's the difference between Security Groups and NACLs?
  **Answer:** Wrong — learner said "NACLs are stateful because they're at a higher level (subnet)"
  **Correction:** It's the opposite. NACLs are STATELESS (must allow both directions explicitly). Security Groups are STATEFUL (return traffic auto-allowed). Higher level ≠ stateful.

- **Difficulty:** NACL stateless behavior — needed 3 examples to understand why outbound ephemeral ports must be explicitly allowed.

- **Breakthrough:** Learner independently calculated that 10.0.0.0/16 = 65,536 IPs by computing 2^(32-16) without prompting.

# Security Policy

This policy applies to every repository in the
[DI-PASSIONATE](https://github.com/DI-PASSIONATE) organisation, unless a repository
ships its own `SECURITY.md`, which then takes precedence.

## Reporting a vulnerability

**Please do not open a public issue, pull request or discussion for a security problem.**

Report it privately instead, in either of these ways:

1. **GitHub private vulnerability reporting** (preferred) - go to the affected
   repository, open the **Security** tab and choose **Report a vulnerability**. This
   keeps the report, our replies and the eventual advisory in one place.
2. **Email** - write to the maintainers of the repository with `SECURITY` in the
   subject line. The E-Mail addresses should be given in the pyproject toml for python projects.

Please include:

- the affected repository, version or commit, and your platform;
- what an attacker can achieve, and what access they need to achieve it;
- reproduction steps, ideally a minimal configuration, netlist or model file;
- any proof-of-concept you have, and whether the issue is already public.

If you need to send something confidential, say so in your first message and we will
arrange a channel.

### What to expect

We are a publicly funded research project, not a vendor with an on-call rotation, so we
answer in working days rather than hours:

| Stage | Target |
| --- | --- |
| Acknowledgement of your report | within 5 working days |
| Initial assessment and severity | within 10 working days |
| Fix or documented mitigation | depends on severity and complexity; we will keep you updated |

We will tell you what we conclude, credit you in the advisory if you would like to be
credited, and coordinate the disclosure date with you. We ask that you give us a
reasonable opportunity to fix the issue before making it public. We do not operate a bug
bounty and cannot offer payment.

## Supported versions

These are research tools under active development. Security fixes go into the **default
branch and the next release only** - there are no long-term support branches, and we do
not backport to older tags. If you are running an older version, the fix is to update.

## Scope and threat model

Please read this before reporting: it tells you what we consider a vulnerability.

Our tools are **local design and simulation tools**. They are meant to be run by an
engineer on their own workstation or compute node, on inputs that engineer trusts. They
are not network services, they have no authentication or multi-tenancy, and they are not
designed to sandbox hostile input.

Consequently, the following are **expected behaviour and not vulnerabilities**:

- Executing a netlist, configuration, mesh, geometry script or ONNX model that you
  supplied. COBRA, for example, imports custom geometry files as Python modules and
  hands netlists to Xyce - anything in those files runs with your privileges, by design.
  **Only run inputs and models you trust or produced yourself**, exactly as you would
  with any script.
- Anything that requires an attacker to already have write access to your working
  directory, your configuration files or your Python environment.
- Resource exhaustion caused by your own simulation settings (a mesh, sweep or
  optimization run that is too large for the machine).

We *are* interested in, and will treat as vulnerabilities:

- code execution or file access triggered by input a user could plausibly believe is
  inert - for example a downloaded surrogate model, a shared results archive, or a
  Touchstone or netlist file received from a third party;
- path traversal or arbitrary file overwrite from a configuration value, a component
  name, or a filename inside an archive we unpack;
- command injection reachable from configuration or netlist content;
- leaking credentials, tokens or private paths into logs, results directories,
  generated files or telemetry;
- vulnerabilities in how ORCA-OpenStack authenticates against or provisions cloud
  resources, or any weakening of the isolation of a deployed VM image;
- a dependency we ship or pin with a known, exploitable vulnerability that is reachable
  through our code.

## Out of scope: upstream tools

We integrate several third-party tools and do not maintain them. A vulnerability in
[Xyce](https://xyce.sandia.gov/), [AWS Palace](https://awslabs.github.io/palace/),
[gmsh](https://gmsh.info/), [Qucs-S](https://ra3xdh.github.io/),
[ONNX Runtime](https://onnxruntime.ai/) or any other dependency should be reported to
that project.

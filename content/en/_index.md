---
title: Flux - the GitOps family of projects
description: > 
  Flux is a set of continuous and progressive delivery solutions for Kubernetes, and they are open and extensible. 
  
  Flux v2 will be GA within the next few months! 
  
  This means that Flux v1 will be deprecated before the end of 2021, so now is a good time to start using v2.
---
{{% blocks/celebration emoji="🎉" url="/blog/2021/03/flux-is-a-cncf-incubation-project/" %}}
Flux is now a CNCF Incubation project!
{{% /blocks/celebration %}}

{{% blocks/hero title="Flux" subtitle="The GitOps family of projects" color="primary"
                height="full"%}}

Flux is a set of continuous and progressive delivery solutions for Kubernetes, and they are open and extensible.

Flux v2 will be GA within the next few months! This means that Flux v1 will be deprecated before the end of 2021, so now is a good time to start using v2.  

{{% button link_url="/docs/get-started/" link_title="Get started" %}}

{{% /blocks/hero %}}

<!-- features -->
<!-- 
{{< blocks/section color="white" >}}

# **GitOps at your fingertips**



{{< /blocks/section >}} -->

{{< blocks/section type="features" color="white" >}}

<div class="col-lg-12 text-center " style="padding-bottom: 80px; margin: 0; padding-left: 10%; padding-right: 10%" >

# **GitOps at your fingertips**

#### Flux is a collection of tools for keeping [Kubernetes](https://kubernetes.io/) clusters in sync with sources of configuration (like Git repositories), and automating updates to configuration when there is new code to deploy.

</div>

{{% blocks/feature icon="fab fa-git-square fa-3x" title="Declarative" height="auto" color="primary" %}}

Describe the entire desired state of your system in [Git](https://git-scm.com). This includes apps, configuration,
dashboards, monitoring, and everything else.

{{% /blocks/feature %}}

{{% blocks/feature icon="fas fa-robot fa-3x" title="Automated" height="auto"%}}

  Use [YAML](https://yaml.org) to enforce conformance to the declared system. 
  You don't need to run [`kubectl`](https://kubectl.docs.kubernetes.io/) because all changes are synced automatically.

{{% /blocks/feature %}}

{{% blocks/feature icon="fas fa-code fa-3x" title="Auditable" height="auto"  %}}

  Everything is controlled through pull requests. Your Git history provides a sequence of transactions, allowing you to
  recover state from any snapshot.

{{% /blocks/feature %}}

{{% blocks/feature icon="fas fa-drafting-compass fa-3x" title="Designed for Kubernetes" height="auto"  %}}

  Declaratively configurable using Custom Resources, state reports in the
  [object's status](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/#object-spec-and-status)
  and via [Kubernetes Events](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-application-introspection/),
  and integrations with Kubernetes RBAC

{{% /blocks/feature %}}

{{% blocks/feature icon="fas fa-box-open fa-3x" title="Out-of-the-box integrations" height="auto" %}}

Support for e.g. [Kustomize](https://kustomize.io), [Helm](https://helm.sh); GitHub, GitLab, Harbor and custom
webhooks; notifications to most team communication platforms; and many more.

{{% /blocks/feature %}}

{{% blocks/feature icon="fas fa-cube fa-3x" title="Extensible" height="auto"%}}

Easily create a continous delivery solution with only the components you need, or use the [GitOps Toolkit](#gitops-toolkit)
to extend Flux.

{{% /blocks/feature %}}

{{< /blocks/section >}}





{{< blocks/section color="light" >}}
<div class="col-lg-12 text-center " style="padding-bottom: 80px; margin: 0; padding-left: 10%; padding-right: 10%" >

# **Resources**
#### New to Flux? Check out some of the resources below!
</div>

{{% blocks/resource
  youtube="nGLpUCPX8JE"
  title="The Evolution of Flux v2 with Stefan Prodan" %}}
Stefan introduces Flux v2, explains why it was reshaped into a composable continuous delivery solution that goes beyond Git sync to accommodate multi-tenancy, infrastructure dependencies and cluster-api fleet management.
{{% /blocks/resource %}}

{{% blocks/resource
  youtube="0v5bjysXTL8"
  title="The Power of GitOps with Flux v2 & GitOps Toolkit with Leigh Capili" %}}
Leigh demos bootstrapping with GitOps Toolkit, app deployment, and monitoring with Prometheus.
{{% /blocks/resource %}}

{{% blocks/resource
  youtube="JcKUawSQfQ0"
  title="Flux v2 for Helm Users with Scott Rigby" %}}
Scott covers what to keep in mind as Helm 2 support ends, the benefits of Helm Controller, and how to migrate from Helm Operator to Helm Controller.
{{% /blocks/resource %}}

{{% blocks/resource
  youtube="7W27tAv7Tvs"
  title="Managing Remote Clusters with Flux v2 (CAPI demo) with Leigh Capili" %}}
Leigh covers cluster API integration, dependency management & ordering, security model updates, and delegation & multi-tenancy via users.
{{% /blocks/resource %}}

{{% blocks/resource
  youtube="R6OeIgb7lUI"
  title="Flux v2 overview, demo, & review with Viktor Farcic" %}}
Stefan introduces Flux v2, explains why it was reshaped into a composable continuous delivery solution that goes beyond Git sync to accommodate multi-tenancy, infrastructure dependencies and cluster-api fleet management.
{{% /blocks/resource %}}

{{% blocks/resource
  youtube="N6UCKF7JD7k"
  title="Flux v2 Deep Dive series with Geert Baeke" %}}
In this 5 video series, Geert Baeke takes a deep dive of Flux v2 and the use of GitOps principles with an Intro to Flux v2, Intro to Kustomize, Deploying Manifests, Monitoring & Alerting, and Helm Basics.
{{% /blocks/resource %}}

{{< /blocks/section >}}


{{< blocks/section color="white" >}}

<div class="col-lg-12 text-center " style="padding-bottom: 80px; margin: 0; padding-left: 10%; padding-right: 10%" >

# **Other Flux projects**

</div>

{{% blocks/project title="GitOps Toolkit"
  image="/img/building-blocks.svg" image-align="left" bg-color="primary"
%}}

The set of APIs and controllers that make up the runtime for Flux. You can use the GitOps Toolkit to extend Flux, and to build your own systems for continuous delivery.

{{% /blocks/project %}}

{{% blocks/project title="Flagger"
  image="/img/flagger-gitops.png" image-align="right" bg-color="green"
%}}

Kubernetes Operator for the automation of promoting canary deployments using Istio, Linkerd, App Mesh, NGINX, Skipper, Contour, Gloo or Traefik routing for traffic shifting, and Prometheus metrics for canary analysis.

The canary analysis can be extended with webhooks for running system integration/acceptance tests, load tests, or any other custom validation.

{{% /blocks/project %}}
  
{{% blocks/project title="Flux v1 and Helm Operator"
  image="/img/logos/flux-horizontal-color.png" image-align="right" bg-color="dark"
 %}}

We owe our success and good reputation as GitOps project to Flux and Helm Operator. They are the v1 iteration of our project and currently in [maintenance mode](https://github.com/fluxcd/flux/issues/3320).

We strongly advise everyone to familiarize themselves with Flux v2 and start the process of migrating.

{{% /blocks/project %}}

{{< /blocks/section >}}

<!-- Community -->
 
{{< blocks/section color="dark" type="community">}}

<div class="col-lg-12 text-center " style="padding-bottom: 80px; margin: 0; padding-left: 10%; padding-right: 10%" >

# **Community**

#### The Flux project aspires to be the vendor-neutral home for GitOps in a Cloud Native world.

#### What we achieved up until today is only possible because of our community.

</div>

<div class="card-deck align-top">

{{% blocks/community icon="fab fa-github fa-3x" title="GitHub Discussions" link_url="https://github.com/fluxcd/flux2/discussions" link_title="flux2 GitHub Discussions" %}}

Join the conversation in GitHub Discussions. Everything Flux v2 related ranging from specificiations and feature planning to Show & Tell happens here.

Join the discussion today!


{{% /blocks/community %}}

{{% blocks/community icon="fab fa-slack fa-3x" title="Slack" link_url="https://slack.cncf.io" link_title="Get your CNCF Slack Invite!" %}}

If you want to talk to the Flux team and community in real-time, join us on Slack. This is a great way to get to know everyone.

Get an invite, or go to the `#flux` channel.

{{% /blocks/community %}}

{{% blocks/community icon="fa fa-paper-plane fa-3x" title="Mailing list" link_url="https://lists.cncf.io/g/cncf-flux-dev" link_title="Join the mailing list!" %}}

Join our (low-traffic) mailing list to stay up to day on announcements and sporadic discussions.

{{% /blocks/community %}}

</div>

{{< /blocks/section >}}

{{< blocks/cncf >}}
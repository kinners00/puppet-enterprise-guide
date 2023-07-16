<div class="tocoutline">

### Table of Contents

<div class="toc">

- [Overview](#overview)
- [Who is this for?](#who-is-this-for)
- [Why does this guide need to exist?](#why-does-this-guide-need-to-exist)
- [Should I use this instead of Puppet docs?](#should-i-use-this-instead-of-puppet-docs)
- [What's in this Guide?](#whats-in-this-guide)
    - [Reference and theory](#reference-and-theory)
    - [Example Walkthroughs](#example-walkthroughs)
    - [Labs](#labs)
- [Roadmap](#roadmap)
- [Who wrote this guide?](#who-wrote-this-guide)
- [Feedback & Reporting issues](#feedback--reporting-issues)

</div>

</div>

# Overview<a href="#overview" aria-hidden="true"></a>
The Puppet Enterprise guide is a practical and opinionated guide on how to get up and running with Puppet Enterprise (PE). The aim is that, by using this guide you'll be confident enough to deploy and manage PE day to day and thus be equipped to tackle any automation task that comes your way. The main goals for this guide is to help you understand:

1. What the tool does
2. When you would use it for specific automation tasks
3. How it works
4. How you use it 

> This guide is a personal project and not endorsed by Puppet.

# Who is this for?<a href="#who-is-this-for" aria-hidden="true"></a>

* Folks starting off with puppet and automation tooling
* OSP users who want to learn PE
* Current PE customers who want to learn more

# Why does this guide need to exist?<a href="#why-does-this-guide-need-to-exist" aria-hidden="true"></a>

One of the benefits of Puppet Enterprise is that it's really flexible. This allows users to leverage PE in lots of different ways and in various configurations and architectures. Whilst this is an advantage, it can also make it difficult to learn. Given that, this guide exists to serve as an opinionated view, following best practice, on how to use PE rather than explaining the many ways that you can use and configure the tool. 

# Should I use this instead of Puppet docs?<a href="#should-i-use-this-instead-of-puppet-docs" aria-hidden="true"></a>

No. This guide should be used in tandem with the official Puppet docs. There is a lot of additional information in the Puppet docs that you'll _not_ get in this guide, given it's scope and purpose, however you'll find that there are links on most pages within the guide that refer directly to the official Puppet docs, where appropriate.

The Puppet Enterprise guide is based off the latest STS (short term support) release of Puppet Enterprise PE 2023.X, however, if you're on the most recent LTS (long term support), 2021.7.X, the majority of the content in this guide will still apply. 

The official PE docs include versioned docs i.e. docs for different Puppet Enterprise releases, which we'd recommend you follow, particulary for upgrades or large complex puppet installations.


# What's in this Guide?<a href="#whats-in-this-guide" aria-hidden="true"></a>

### Labs<a href="#labs" aria-hidden="true"></a>
The labs are a great way to get to know Puppet Enterprise more intimately in a lab based environment. There are examples for both Windows and Linux based targets for every lab topic. If you're starting off with PE, we'd recommend that you follow the lab track to gain a good understanding of how PE works.

### Reference and theory<a href="#reference-and-theory" aria-hidden="true"></a>
 
These pages contain topics such as: feature and capability overviews, benefits, usecases, how it works and more. All topic sections begin with at least 1 reference/theory page. Each topic will include some basic "how to" information.

### Example Walkthroughs<a href="#example-walkthroughs" aria-hidden="true"></a>
These are step-by-step guided walkthroughs, from creation to end state. These walkthroughs show the process behind creating a configuration, desired state or adhoc automation - rather than only providing an example configuration. Task and Plan walkthroughs include Windows and Linux examples.

# Who wrote this guide?<a href="#who-wrote-this-guide" aria-hidden="true"></a>

* Marc McKinley
  - **Role:** Senior Sales Engineer EMEA, Puppet
  - **Tenure:** 5yrs 
  - **Contribution:** Content and Review, Website and Design


* Kevin Reeuwijk
  - **Role:** Senior Manager Sales Engineering EMEA, Puppet
  - **Tenure:** 4yrs 
  - **Contribution:** Content and Review


# Feedback & Reporting issues<a href="#feedback--reporting-issues" aria-hidden="true"></a>
Feedback is very much welcome. We want to ensure this guide is as useful as can be, so if you see something that doesn't make sense, such as an error or if you'd like to see a topic covered in the guide, feel free to file a request <a href="https://github.com/kinners00/puppet-enterprise-guide/issues" target="_blank">here</a>.
